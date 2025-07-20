<script setup>
import { ref, computed } from 'vue'
import QuestionCard from './QuestionCard.vue'
import ScoreBoard from './ScoreBoard.vue'
import ResultScreen from './ResultScreen.vue'
import ScreenReaderAnnouncer from './ScreenReaderAnnouncer.vue'
import { questions } from '../data/questions.js'

const emit = defineEmits(['quiz-complete'])

const currentQuestionIndex = ref(0)
const score = ref(0)
const selectedAnswers = ref([])
const isQuizComplete = ref(false)
const shuffledQuestions = ref([])
const announcementMessage = ref('')

const shuffleArray = (array) => {
  const newArray = [...array]
  for (let i = newArray.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[newArray[i], newArray[j]] = [newArray[j], newArray[i]]
  }
  return newArray
}

shuffledQuestions.value = shuffleArray(questions).slice(0, 10)

const currentQuestion = computed(() => {
  return shuffledQuestions.value[currentQuestionIndex.value]
})

const progress = computed(() => {
  return ((currentQuestionIndex.value + 1) / shuffledQuestions.value.length) * 100
})

const handleAnswer = (answerIndex) => {
  selectedAnswers.value.push({
    questionId: currentQuestion.value.id,
    answer: answerIndex,
    isCorrect: answerIndex === currentQuestion.value.correct
  })
  
  if (answerIndex === currentQuestion.value.correct) {
    score.value++
    announcementMessage.value = 'Correct! Well done!'
  } else {
    announcementMessage.value = `Incorrect. The correct answer is: ${currentQuestion.value.options[currentQuestion.value.correct]}`
  }
  
  setTimeout(() => {
    if (currentQuestionIndex.value < shuffledQuestions.value.length - 1) {      
      currentQuestionIndex.value++
    } else {
      isQuizComplete.value = true
    }

    // Clear after announcement to allow same message to be announced again
    announcementMessage.value = ''
  }, 3000)
}

const restartQuiz = () => {
  emit('quiz-complete')
}
</script>

<template>
  <div class="quiz-container">
    <ScreenReaderAnnouncer :message="announcementMessage" />
    
    <ScoreBoard 
      v-if="!isQuizComplete"
      :score="score"
      :totalQuestions="shuffledQuestions.length"
      :currentQuestion="currentQuestionIndex + 1"
      :progress="progress"
    />
    
    <QuestionCard
      v-if="!isQuizComplete && currentQuestion"
      :question="currentQuestion"
      @answer="handleAnswer"
      :key="currentQuestion.id"
    />
    
    <ResultScreen
      v-if="isQuizComplete"
      :score="score"
      :totalQuestions="shuffledQuestions.length"
      :answers="selectedAnswers"
      @restart="restartQuiz"
    />
  </div>
</template>

<style scoped>
.quiz-container {
  width: 100%;
  max-width: 700px;
  margin: 0 auto;
}
</style>