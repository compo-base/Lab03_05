<template>
  <h1>Sorry</h1>
  <h3>We dont have resorce that you want</h3>
</template>

<script setup lang="ts">
defineProps({
  resource: {
    type: String,
    required: true,
    default: 'page'
  }
})
</script>
