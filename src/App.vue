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

<style scoped>
.app {
  max-width: 900px;
  margin: 28px auto;
  padding: 20px;
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 6px 18px rgba(16, 24, 40, 0.06);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  margin-bottom: 18px;
}

.input {
  padding: 8px 12px;
  border-radius: 8px;
  border: 1px solid #e5e7eb;
  width: 260px;
}
</style>