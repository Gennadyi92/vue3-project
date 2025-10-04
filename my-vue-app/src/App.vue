<template>
  <div>
    <h1>Телефонный справочник</h1>
    <ContactForm :contact="currentContact" :isEditing="isEditing" @submit="handleSubmit" />
    <ContactList :contacts="contacts" @delete="deleteContact" @edit="editContact" />
  </div>
</template>

<script>
import ContactForm from './components/ContactForm.vue';
import ContactList from './components/ContactList.vue';

export default {
  components: {
    ContactForm,
    ContactList
  },
  data() {
    return {
      contacts: [
        { id: 1, name: 'Иван Иванов', phone: '123-456-7890' },
        { id: 2, name: 'Петр Петров', phone: '987-654-3210' }
      ],
      currentContact: {},
      isEditing: false
    };
  },
  methods: {
    handleSubmit(contact) {
      if (this.isEditing) {
        const index = this.contacts.findIndex(c => c.id === contact.id);
        this.contacts.splice(index, 1, contact);
        this.isEditing = false;
      } else {
        contact.id = Date.now();
        this.contacts.push(contact);
      }
      this.currentContact = {};
    },
    deleteContact(contact) {
      const index = this.contacts.findIndex(c => c.id === contact.id);
      this.contacts.splice(index, 1);
    },
    editContact(contact) {
      this.currentContact = { ...contact };
      this.isEditing = true;
    }
  }
}
</script>