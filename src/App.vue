<template>
  <div class="app">
    <div class="header">
      <h2>Список пользователей</h2>
      <input v-model="search" class="input" placeholder="Поиск по имени..." />
    </div>

    <UserList :search-term="search" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import UserList from './components/UserList.vue'

const search = ref('')
</script>
