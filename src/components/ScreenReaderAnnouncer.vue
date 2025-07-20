<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  message: {
    type: String,
    default: ''
  }
})

const announcement = ref('')

watch(() => props.message, (newMessage) => {
  if (newMessage) {
    announcement.value = newMessage
    // Clear after announcement to allow same message to be announced again
    setTimeout(() => {
      announcement.value = ''
    }, 100)
  }
})
</script>

<template>
  <div class="sr-only" aria-live="assertive" aria-atomic="true">
    {{ announcement }}
  </div>
</template>