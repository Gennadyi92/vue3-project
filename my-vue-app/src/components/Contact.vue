<template>
  <li>
    <span>{{ contact.name }}: {{ contact.phone }}</span>
    <button @click="editContact">Редактировать</button>
    <button @click="deleteContact">Удалить</button>
  </li>
</template>

<script>
export default {
  props: {
    contact: Object
  },
  methods: {
    editContact() {
      this.$emit('edit', this.contact);
    },
    deleteContact() {
      this.$emit('delete', this.contact);
    }
  }
}
</script>