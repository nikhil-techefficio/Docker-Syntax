<script setup>
import { ref, onMounted } from 'vue'

const message = ref('Loading...')

onMounted(async () => {
  const response = await fetch(
    'http://backend-service:5000/api/health'
  )

  const data = await response.json()

  message.value = data.status
})
</script>

<template>
  <h1>{{ message }}</h1>
</template>