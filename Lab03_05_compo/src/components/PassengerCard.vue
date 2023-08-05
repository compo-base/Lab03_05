<template>
  <div class="passenger-card">
    <h3>{{ passenger.first_name }} {{ passenger.last_name }}</h3>
    <p>{{ passenger.email }}</p>
  </div>
</template>

<script setup lang="ts">
import { props } from 'vue'
import type { PassengerInfo } from '@/type'

// Define props for the component
const props = defineProps({
  passenger: {
    type: Object as () => PassengerInfo,
    required: true
  }
})
</script>

<style scoped>
.passenger-card {
  border: 1px solid #ddd;
  padding: 10px;
  margin: 10px 0;
}
</style>
