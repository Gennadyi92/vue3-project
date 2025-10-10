<!-- src/components/PhoneBook.vue -->
<template>
  <div>
    <h1>Телефонный справочник</h1>
    <div class="search-bar">
      <input type="text" placeholder="Поиск" v-model="searchQuery" />
      <button @click="performSearch">Поиск</button>
    </div>
    <ContactForm @addContact="addContact" @updateContact="updateContact" />
    <ContactList :contacts="filteredContacts" @deleteContact="deleteContact" />
  </div>
</template>

<script setup>
import { reactive, computed } from 'vue';
import ContactList from './ContactList.vue';
import ContactForm from './ContactForm.vue';

const state = reactive({
  contacts: [
    { id: 1, name: 'Иван Иванов', phone: '+7 911 123-45-67' },
    { id: 2, name: 'Анна Смирнова', phone: '+7 921 987-65-43' },
    { id: 3, name: 'Сергей Кузнецов', phone: '+7 931 555-12-34' },
    { id: 4, name: 'Елена Петрова', phone: '+7 941 777-98-76' },
    { id: 5, name: 'Дмитрий Сидоров', phone: '+7 951 333-44-55' },
    { id: 6, name: 'Марина Васильева', phone: '+7 961 888-11-22' },
    { id: 7, name: 'Алексей Орлов', phone: '+7 971 666-77-88' },
    { id: 8, name: 'Ольга Лебедева', phone: '+7 981 222-33-44' },
    { id: 9, name: 'Николай Кузнецов', phone: '+7 991 444-55-66' },
    { id: 10, name: 'Светлана Морозова', phone: '+7 901 999-88-77' }
  ],
  searchQuery: ''
});

const filteredContacts = computed(() => {
  return state.contacts.filter(contact => {
    return contact.name.toLowerCase().includes(state.searchQuery.toLowerCase());
  });
});

const performSearch = () => {
  state.searchQuery = ''; // Очищаем поле поиска после нажатия кнопки
};

const addContact = (contact) => {
  const newId = Date.now();
  state.contacts.push({ id: newId, ...contact });
};

const updateContact = (contact) => {
  const index = state.contacts.findIndex(c => c.id === contact.id);
  if (index !== -1) {
    state.contacts[index] = contact;
  }
};

const deleteContact = (id) => {
  state.contacts = state.contacts.filter(contact => contact.id !== id);
};
</script>

<style scoped>
.search-bar {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.search-bar input {
  flex: 1;
  margin-right: 10px;
  padding: 5px;
}

.search-bar button {
  padding: 5px 10px;
}
</style>