<template>
  <h1>Recap</h1>
</template>

<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  quiz: Object,
  answers: Array,
})
</script>
