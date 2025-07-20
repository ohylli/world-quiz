<script setup>
import { ref } from 'vue'

const props = defineProps({
  question: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['answer'])

const selectedAnswer = ref(null)
const showFeedback = ref(false)

const selectAnswer = (index) => {
  if (selectedAnswer.value !== null) return
  
  selectedAnswer.value = index
  showFeedback.value = true
  emit('answer', index)
}

const getButtonClass = (index) => {
  if (!showFeedback.value) return 'option-button'
  
  if (index === props.question.correct) {
    return 'option-button correct'
  }
  
  if (index === selectedAnswer.value && index !== props.question.correct) {
    return 'option-button incorrect'
  }
  
  return 'option-button'
}
</script>

<template>
  <div class="question-card">
    <h2 class="question-text" role="alert" aria-live="assertive" aria-atomic="true">{{ question.question }}</h2>
    
    <div class="options-grid">
      <button
        v-for="(option, index) in question.options"
        :key="index"
        :class="getButtonClass(index)"
        :disabled="selectedAnswer !== null"
        @click="selectAnswer(index)"
      >
        {{ option }}
      </button>
    </div>
    
    <div v-if="showFeedback" class="feedback">
      <p v-if="selectedAnswer === question.correct" class="correct-feedback">
        Correct! Well done!
      </p>
      <p v-else class="incorrect-feedback">
        Incorrect. The correct answer is: {{ question.options[question.correct] }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.question-card {
  background: white;
  border-radius: 12px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin-top: 2rem;
}

.question-text {
  font-size: 1.4rem;
  color: #2c3e50;
  margin-bottom: 2rem;
  text-align: center;
}

.options-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.option-button {
  padding: 1rem 1.5rem;
  border: 2px solid #e1e8ed;
  border-radius: 8px;
  background: white;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.option-button:hover:not(:disabled) {
  border-color: #3498db;
  transform: translateY(-2px);
}

.option-button:disabled {
  cursor: not-allowed;
}

.option-button.correct {
  background: #27ae60;
  color: white;
  border-color: #27ae60;
}

.option-button.incorrect {
  background: #e74c3c;
  color: white;
  border-color: #e74c3c;
}

.feedback {
  text-align: center;
  padding: 1rem;
  border-radius: 8px;
  margin-top: 1rem;
}

.correct-feedback {
  color: #27ae60;
  font-weight: 600;
}

.incorrect-feedback {
  color: #e74c3c;
  font-weight: 600;
}

@media (max-width: 600px) {
  .question-card {
    padding: 1.5rem;
  }
  
  .question-text {
    font-size: 1.2rem;
  }
  
  .options-grid {
    grid-template-columns: 1fr;
  }
}
</style>