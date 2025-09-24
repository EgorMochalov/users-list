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

<style scoped>
.users-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 12px;
}

.center { text-align: center; }

.spinner {
  width: 36px;
  height: 36px;
  border: 4px solid #e6eef6;
  border-top-color: #3b82f6;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 20px auto;
}

@keyframes spin { to { transform: rotate(360deg); } }

.error {
  color: #dc2626;
  background: #fff1f2;
  padding: 10px;
  border-radius: 6px;
}
</style>