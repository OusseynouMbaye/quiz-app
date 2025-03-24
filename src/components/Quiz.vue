<template>
  <div>
    <h1>{{ quiz.title }}</h1>
    <Progress :value="step" :max="quiz.questions.length - 1" />
    <Question
      :key="question.question"
      :question="question"
      v-if="quizState === 'question'"
      @answer="addAnswer"
    />
    <Recap v-if="quizState === 'recap'" :answers="answers" :quiz="quiz" />
    <!-- {{ answers }} -->
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'
import Progress from './Progress.vue'
import Question from './Question.vue'
import Recap from './Recap.vue'

const props = defineProps({
  quiz: Object,
  state: String,
})

const quizState = ref('question')
const answers = ref(props.quiz.questions.map(() => null))
const step = ref(0)
const question = computed(() => props.quiz.questions[step.value])
const addAnswer = (answer) => {
  answers.value[step.value] = answer
  if (step.value === props.quiz.questions.length - 1) {
    quizState.value = 'recap'
  } else {
    step.value++
  }
  // step.value++
}
</script>
