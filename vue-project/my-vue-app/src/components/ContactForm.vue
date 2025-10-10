<!-- src/components/ContactForm.vue -->
<template>
  <form @submit.prevent="submitForm">
    <label for="nameInput">Имя:</label>
    <input type="text" id="nameInput" placeholder="Имя" v-model="formName"/>
    
    <label for="phoneInput">Телефон:</label>
    <input type="tel" id="phoneInput" placeholder="Телефон" v-model="formPhone"/>
    
    <button type="submit">{{ isEdit ? 'Сохранить' : 'Добавить' }}</button>
    <button v-if="isEdit" @click="cancelEdit">Отмена</button>
  </form>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({
  contact: {
    type: Object,
    default: null
  }
});

const emit = defineEmits(['addContact', 'updateContact', 'cancelEdit']);

const formName = ref(props.contact ? props.contact.name : '');
const formPhone = ref(props.contact ? props.contact.phone : '');

const isEdit = ref(props.contact !== null);

const submitForm = () => {
  if (isEdit.value) {
    emit('updateContact', {
      id: props.contact.id,
      name: formName.value,
      phone: formPhone.value
    });
  } else {
    emit('addContact', {
      name: formName.value,
      phone: formPhone.value
    });
  }
  formName.value = '';
  formPhone.value = '';
};

const cancelEdit = () => {
  emit('cancelEdit');
};
</script>