<script setup>
defineProps({
  score: {
    type: Number,
    required: true
  },
  totalQuestions: {
    type: Number,
    required: true
  },
  currentQuestion: {
    type: Number,
    required: true
  },
  progress: {
    type: Number,
    required: true
  }
})
</script>

<template>
  <div class="scoreboard">
    <div class="score-info">
      <div class="info-item">
        <span class="label">Question</span>
        <span class="value">{{ currentQuestion }} / {{ totalQuestions }}</span>
      </div>
      <div class="info-item">
        <span class="label">Score</span>
        <span class="value">{{ score }}</span>
      </div>
    </div>
    
    <div class="progress-bar">
      <div class="progress-fill" :style="{ width: progress + '%' }"></div>
    </div>
  </div>
</template>

<style scoped>
.scoreboard {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.score-info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.info-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.label {
  font-size: 0.9rem;
  color: #7f8c8d;
  margin-bottom: 0.25rem;
}

.value {
  font-size: 1.5rem;
  font-weight: 600;
  color: #2c3e50;
}

.progress-bar {
  width: 100%;
  height: 8px;
  background: #ecf0f1;
  border-radius: 4px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: #3498db;
  transition: width 0.3s ease;
  border-radius: 4px;
}
</style>