<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in question.choices" :key="choice">
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
const props = defineProps({
  question: Object,
})

const emits = defineEmits(['answer'])
const answer = ref(null)
const hasAnswer = computed(() => answer.value !== null)
// watch(() => props.question, () => {
//   answer.value = null
// })
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
