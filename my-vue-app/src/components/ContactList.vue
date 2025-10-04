<template>
  <ul>
    <Contact v-for="contact in contacts" :key="contact.id" :contact="contact" @delete="deleteContact" />
  </ul>
</template>

<script>
import Contact from './Contact.vue';

export default {
  components: {
    Contact
  },
  props: {
    contacts: Array
  },
  methods: {
    deleteContact(contact) {
      this.$emit('delete', contact);
    }
  }
}
</script>