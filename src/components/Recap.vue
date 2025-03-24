<template>
  <h1>Recap</h1>
  <p v-if="hasWon">{{ hasWon ? quiz.success_message : quiz.failure_message }}</p>
  <p>You scored {{ score }} out of {{ quiz.questions.length }}</p>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps({
  quiz: Object,
  answers: Array,
})

const score = computed(() => {
  return props.quiz.questions.reduce((acc, question, index) => {
    return question.correct_answer === props.answers[index] ? acc + 1 : acc
  }, 0)
})

const hasWon = computed(() => score.value >= props.quiz.minimum_score)
</script>
