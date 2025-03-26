<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    {{ timer }}
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice">
        <Answer
          :disabled="hasAnswer"
          :id="`answer${index}`"
          :value="choice"
          @change="onAnswer"
          v-model="answer"
          :correctAnswer="question.correct_answer"
        />
      </li>
    </ul>
    <!-- <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button> -->
  </div>
</template>
<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { shuffleArray } from '@/functions/array.js'
import Answer from './Answer.vue'
const props = defineProps({
  question: Object,
})

const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)

const randomChoices = computed(() => shuffleArray(props.question.choices))

let timer

const onAnswer = () => {
  clearInterval(timer)
  timer = setTimeout(() => {
    emits('answer', answer.value)
  }, 1_500)
}

onMounted(() => {
  timer = setTimeout(() => {
    emits('answer', answer.value)
  }, 5_000)
})

onUnmounted(() => {
  clearTimeout(timer)
})
</script>
<style scoped>
.question {
  padding-top: 2rem;

  ul li {
    list-style-type: none;
    padding: 0;
  }
  button {
    margin-left: auto;
    display: block;
  }
}
</style>
<!-- onMounted(() => {
  timer = setInterval(() => {
    if (hasAnswer.value) {
      clearInterval(timer)
      emits('answer', answer.value)
    }
  }, 3_000)
}) -->
