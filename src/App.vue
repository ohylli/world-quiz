<script setup>
import { ref } from 'vue'
import QuizContainer from './components/QuizContainer.vue'

const isQuizActive = ref(false)

const startQuiz = () => {
  isQuizActive.value = true
}

const resetQuiz = () => {
  isQuizActive.value = false
}
</script>

<template>
  <div class="app">
    <header>
      <h1>World Geography Quiz</h1>
    </header>
    
    <main>
      <div v-if="!isQuizActive" class="welcome">
        <h2>Test Your Geography Knowledge!</h2>
        <p>Answer questions about capitals, countries, and more.</p>
        <button @click="startQuiz" class="start-button">Start Quiz</button>
      </div>
      
      <QuizContainer v-else @quiz-complete="resetQuiz" />
    </main>
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
}

header {
  text-align: center;
  margin-bottom: 2rem;
}

h1 {
  color: #2c3e50;
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
}

.welcome {
  text-align: center;
  max-width: 600px;
}

h2 {
  color: #34495e;
  margin-bottom: 1rem;
}

p {
  color: #7f8c8d;
  font-size: 1.1rem;
  margin-bottom: 2rem;
}

.start-button {
  background: #3498db;
  color: white;
  border: none;
  padding: 1rem 2rem;
  font-size: 1.2rem;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s;
}

.start-button:hover {
  background: #2980b9;
}

main {
  flex: 1;
  width: 100%;
  max-width: 800px;
}
</style>
