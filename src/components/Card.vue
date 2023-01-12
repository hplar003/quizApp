<script setup>
  import { useRouter } from "vue-router";
  const { quiz } = defineProps(["quiz"]);

  const router = useRouter();

  const navigateToQuiz = () => {
    router.push(`quiz/${quiz.id}`);
  };
</script>

<template>
  <div>
    <div class="card" @click="navigateToQuiz">
      <img :src="quiz.img" alt="" />
      <div class="card-text">
        <h2>{{ quiz.name }}</h2>
        <p>{{ quiz.questions.length }} Questions</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .card {
    width: 310px;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: rgb(38, 57, 77) 0px 20px 30px -10px;
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;
  }
  .card img {
    width: 100%;
    height: 190px;
    margin: 0;
  }
  .card .card-text {
    padding: 0 5px;
  }
  .card .card-text h2 {
    font-weight: bold;
  }
</style>
