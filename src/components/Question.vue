<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice">
        <label :for="`answer${index}`">
          <input
            :id="`answer${index}`"
            name="answer"
            type="radio"
            v-model="answer"
            :value="choice"
          />{{ choice }}
        </label>
      </li>
    </ul>
    <button :disabled="!hasAnswer" @click="emits('answer', answer)">Question suivante</button>
  </div>
</template>
<script setup>
import { ref, computed, watch } from 'vue'
import { shuffleArray } from '@/functions/array.js'
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
