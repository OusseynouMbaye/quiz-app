<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice">
        <Answer
          :disabled="hasAnswer"
          :id="`answer${index}`"
          :value="choice"
          v-model="answer"
          :correctAnswer="question.correct_answer"
        />
      </li>
    </ul>
    <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>
  </div>
</template>
<script setup>
import { ref, computed, watch } from 'vue'
import { shuffleArray } from '@/functions/array.js'
import Answer from './Answer.vue'
const props = defineProps({
  question: Object,
})

const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)

const randomChoices = computed(() => shuffleArray(props.question.choices))
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
