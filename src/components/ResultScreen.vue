<script setup>
import { computed } from 'vue'

const props = defineProps({
  score: {
    type: Number,
    required: true
  },
  totalQuestions: {
    type: Number,
    required: true
  },
  answers: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['restart'])

const percentage = computed(() => {
  return Math.round((props.score / props.totalQuestions) * 100)
})

const getMessage = computed(() => {
  const percent = percentage.value
  if (percent === 100) return "Perfect! You're a geography master!"
  if (percent >= 80) return "Excellent work! You really know your geography!"
  if (percent >= 60) return "Good job! Keep learning and you'll improve!"
  if (percent >= 40) return "Not bad! There's room for improvement."
  return "Keep practicing! Geography is fun to learn!"
})

const getEmojiForScore = computed(() => {
  const percent = percentage.value
  if (percent === 100) return "🏆"
  if (percent >= 80) return "🌟"
  if (percent >= 60) return "👍"
  if (percent >= 40) return "📚"
  return "💪"
})
</script>

<template>
  <div class="result-screen">
    <div class="result-card">
      <h2>Quiz Complete!</h2>
      
      <div class="score-display">
        <div class="emoji">{{ getEmojiForScore }}</div>
        <div class="score-text">
          <span class="score-number">{{ score }}</span>
          <span class="score-divider">/</span>
          <span class="total-number">{{ totalQuestions }}</span>
        </div>
        <div class="percentage">{{ percentage }}%</div>
      </div>
      
      <p class="message">{{ getMessage }}</p>
      
      <div class="result-summary">
        <div class="summary-item correct">
          <span class="summary-label">Correct Answers</span>
          <span class="summary-value">{{ score }}</span>
        </div>
        <div class="summary-item incorrect">
          <span class="summary-label">Incorrect Answers</span>
          <span class="summary-value">{{ totalQuestions - score }}</span>
        </div>
      </div>
      
      <button @click="$emit('restart')" class="restart-button">
        Play Again
      </button>
    </div>
  </div>
</template>

<style scoped>
.result-screen {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 400px;
}

.result-card {
  background: white;
  border-radius: 12px;
  padding: 3rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
  max-width: 500px;
  width: 100%;
}

h2 {
  color: #2c3e50;
  font-size: 2rem;
  margin-bottom: 2rem;
}

.score-display {
  margin-bottom: 1.5rem;
}

.emoji {
  font-size: 4rem;
  margin-bottom: 1rem;
}

.score-text {
  font-size: 3rem;
  font-weight: 700;
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.score-number {
  color: #3498db;
}

.score-divider {
  margin: 0 0.5rem;
  color: #7f8c8d;
}

.total-number {
  color: #7f8c8d;
}

.percentage {
  font-size: 2rem;
  font-weight: 600;
  color: #3498db;
}

.message {
  font-size: 1.2rem;
  color: #34495e;
  margin-bottom: 2rem;
}

.result-summary {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 2rem;
}

.summary-item {
  padding: 1rem;
  border-radius: 8px;
}

.summary-item.correct {
  background: #d4edda;
}

.summary-item.incorrect {
  background: #f8d7da;
}

.summary-label {
  display: block;
  font-size: 0.9rem;
  color: #7f8c8d;
  margin-bottom: 0.5rem;
}

.summary-value {
  display: block;
  font-size: 1.8rem;
  font-weight: 600;
}

.summary-item.correct .summary-value {
  color: #27ae60;
}

.summary-item.incorrect .summary-value {
  color: #e74c3c;
}

.restart-button {
  background: #3498db;
  color: white;
  border: none;
  padding: 1rem 2rem;
  font-size: 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s;
}

.restart-button:hover {
  background: #2980b9;
}

@media (max-width: 600px) {
  .result-card {
    padding: 2rem;
  }
  
  h2 {
    font-size: 1.5rem;
  }
  
  .emoji {
    font-size: 3rem;
  }
  
  .score-text {
    font-size: 2.5rem;
  }
  
  .percentage {
    font-size: 1.5rem;
  }
}
</style>