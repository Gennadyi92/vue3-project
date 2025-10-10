<!-- src/components/ContactList.vue -->
<template>
  <ul>
    <li v-for="contact in contacts" :key="contact.id">
      <span v-if="!contact.isEditing">
        {{ contact.name }} — {{ contact.phone }}
        <button @click="editContact(contact)">Редактировать</button>
        <button @click="deleteContact(contact.id)">Удалить</button>
      </span>
      <ContactForm v-else :contact="contact" @updateContact="updateContact" @cancelEdit="cancelEdit(contact)" />
    </li>
  </ul>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
import ContactForm from './ContactForm.vue';

const props = defineProps({
  contacts: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['deleteContact', 'updateContact']);

const editContact = (contact) => {
  contact.isEditing = true;
};

const updateContact = (updatedContact) => {
  emit('updateContact', updatedContact);
  updatedContact.isEditing = false;
};

const cancelEdit = (contact) => {
  contact.isEditing = false;
};

const deleteContact = (id) => {
  emit('deleteContact', id);
};
</script>