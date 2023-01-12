<script setup>
  import Question from "../components/Question.vue";
  import QuizHeader from "../components/QuizHeader.vue";
  import Result from "../components/Result.vue";
  import { useRoute } from "vue-router";
  import data from "../data/data.json";
  import { watch, ref, computed } from "vue";

  const route = useRoute();
  const quizID = parseInt(route.params.id);
  const currentQuestionIndex = ref(0);
  const quiz = data.find((q) => q.id === quizID);
  const numberOfCorrectAnswer = ref(0);
  const showResult = ref(false);

  const questionStatus = computed(
    () => `${currentQuestionIndex.value}/${quiz.questions.length}`
  );
  const barPercentage = computed(
    () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
  );

  const onOptionSelected = (isCorrect) => {
    console.log("emitted event" + isCorrect);
    if (isCorrect) {
      numberOfCorrectAnswer.value++;
    }
    if (quiz.questions.length - 1 === currentQuestionIndex.value) {
      showResult.value = true;
    }
    currentQuestionIndex.value++;
  };
</script>
<template>
  <div class="container">
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
        v-if="!showResult"
      />
      <Result
        v-else
        :quizQuestionLength="quiz.questions.length"
        :numberOfCorrectAnswer="numberOfCorrectAnswer"
      />
    </div>
  </div>
</template>

<style scoped></style>
