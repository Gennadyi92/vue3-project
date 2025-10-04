<template>
  <form @submit.prevent="submit">
    <input v-model="contact.name" placeholder="Имя" required>
    <input v-model="contact.phone" placeholder="Телефон" required>
    <button type="submit">{{ isEditing ? 'Сохранить' : 'Добавить' }}</button>
  </form>
</template>

<script>
export default {
  props: {
    contact: Object,
    isEditing: Boolean
  },
  methods: {
    submit() {
      this.$emit('submit', this.contact);
    }
  }
}
</script>