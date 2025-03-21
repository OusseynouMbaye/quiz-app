<template>
  <div class="container">
    <div v-if="state === 'error'"><p>Impossible de charger le quiz</p></div>
    <div :aria-busy="state === 'loading'">
      <Quiz :quiz="quiz" v-if="quiz" />
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Quiz from '../components/Quiz.vue'

const quiz = ref(null)
const state = ref('loading')

onMounted(() => {
  fetch('/quiz.json')
    .then((response) => {
      if (response.ok) {
        return response.json()
      }
      throw new Error('Network response was not ok')
    })
    .then((data) => {
      quiz.value = data
      state.value = 'idle'
    })
    .catch((error) => {
      console.error('There has been a problem with your fetch operation:', error)
      state.value = 'error'
    })
})
</script>
<style>
.container {
  margin-block: 2rem;
}
</style>
