<script setup>
const props = defineProps({
  message: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div class="sr-only" role="alert" aria-live="assertive" aria-atomic="true">
    {{ message }}
  </div>
</template>