<template>
  <div>
    <div v-if="loading" class="center">
      <div class="spinner" aria-hidden="true"></div>
    </div>

    <div v-else-if="error" class="error">
      Ошибка при загрузке данных: {{ error }}
    </div>

    <div v-else>
      <div v-if="filteredUsers.length === 0" class="small center">Пользователи не найдены.</div>
      <div class="users-grid">
        <UserCard v-for="user in filteredUsers" :key="user.id" :user="user" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, watch } from 'vue'
import UserCard from './UserCard.vue'

const props = defineProps({
  searchTerm: { type: String, default: '' }
})

const users = ref([])
const loading = ref(false)
const error = ref('')

async function fetchUsers() {
  loading.value = true
  error.value = ''
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/users')
    if (!res.ok) throw new Error(`HTTP ${res.status}`)
    users.value = await res.json()
  } catch (err) {
    error.value = err.message || 'Unknown error'
  } finally {
    loading.value = false
  }
}

onMounted(fetchUsers)

const filteredUsers = computed(() => {
  const q = props.searchTerm.trim().toLowerCase()
  if (!q) return users.value
  return users.value.filter(u => u.name.toLowerCase().includes(q))
})
</script>