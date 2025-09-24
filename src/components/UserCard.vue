<template>
  <div class="card">
    <div class="name">{{ user.name }}</div>
    <div class="small">{{ user.email }}</div>
    <div class="small">Город: {{ user.address?.city || '—' }}</div>
  </div>
</template>

<script setup>
const props = defineProps({ user: { type: Object, required: true } })
</script>

<style scoped>
.card {
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #e6eef6;
  background: linear-gradient(180deg, #ffffff, #fbfdff);
}

.name {
  font-weight: 600;
  margin-bottom: 6px;
}
</style>