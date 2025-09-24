<template>
  <div class="card">
    <div style="font-weight:600">{{ user.name }}</div>
    <div class="small">{{ user.email }}</div>
    <div class="small">Город: {{ user.address?.city || '—' }}</div>
  </div>
</template>

<script setup>
const props = defineProps({ user: { type: Object, required: true } })
</script>