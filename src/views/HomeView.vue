<script setup>
  import data from "../data/data.json";
  import { ref, watch } from "vue";
  import Card from "../components/Card.vue";

  const quizes = ref([]);
  quizes.value = data;

  const search = ref("");
  watch(search, () => {
    quizes.value = data.filter((quiz) =>
      quiz.name.toLowerCase().includes(search.value.toLowerCase())
    );
  });
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1>Quiz</h1>
        <input v-model.trim="search" type="text" placeholder="Search..." />
      </header>
      <div class="options-container">
        <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
      </div>
    </div>
  </main>
</template>

<style scoped>
  .container {
    max-width: 1000px;
    margin: 0 auto;
  }
  header {
    margin-bottom: 10px;
    margin-top: 30px;
    display: flex;
    align-items: center;
  }
  header h1 {
    font-weight: bold;
    margin-right: 30px;
  }
  header input {
    border: none;
    background: rgba(230, 228, 228, 0.6);
    padding: 10px;
    border-radius: 5px;
  }
  .options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  }

  /* Card */
</style>
