<script setup>
  import { ref } from "vue";
  const { numberOfCorrectAnswer, quizQuestionLength } = defineProps([
    "numberOfCorrectAnswer",
    "quizQuestionLength",
  ]);

  const color = ref("");
  if (numberOfCorrectAnswer < quizQuestionLength) {
    color.value = "Red";
  } else {
    color.value = "Blue";
  }
</script>
<template>
  <div class="results">
    <p>Your result ...</p>
    <h1>{{ numberOfCorrectAnswer }} / {{ quizQuestionLength }}</h1>
  </div>
</template>

<style scoped>
  .results {
    text-align: center;
    padding: 100px 0;
  }
  .results p {
    font-size: 25px;
  }
  .results h1 {
    font-size: 80px;
    color: v-bind(color);
  }
</style>
