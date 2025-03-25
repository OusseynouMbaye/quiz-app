<template>
  <label :for="id" :class="classes">
    <input
      :disabled="disabled"
      :id="id"
      name="answer"
      type="radio"
      v-model="model"
      :value="value"
    />{{ value }}
  </label>
</template>
<script setup>
import { computed } from 'vue'
const props = defineProps({
  id: String,
  disabled: Boolean,
  value: String,
  correctAnswer: String,
})
const model = defineModel()

const classes = computed(() => ({
  disabled: props.disabled,
  correct: props.disabled && props.value === props.correctAnswer,
  incorrect: props.disabled && props.value !== props.correctAnswer && model.value === props.value,
}))
</script>

<style>
.disabled {
  opacity: 0.5;
}
.correct {
  color: green;
  opacity: 1;
}
.incorrect {
  color: red;
}
</style>
