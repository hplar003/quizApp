<script setup>
  import data from "../data/data.json";
  import { ref, watch } from "vue";
  import Card from "../components/Card.vue";
  import gsap from "gsap";

  const quizes = ref([]);
  quizes.value = data;

  const search = ref("");
  watch(search, () => {
    quizes.value = data.filter((quiz) =>
      quiz.name.toLowerCase().includes(search.value.toLowerCase())
    );
  });
  const beforeEnter = (el) => {
    el.style.opacity = 0;
    el.style.transform = "translateY(-100px)";
  };
  const enter = (el) => {
    gsap.to(el, {
      y: 0,
      opacity: 1,
      duration: 0.8,
      delay: el.dataset.index * 0.8,
    });
  };
  const afterEnter = (el) => {};
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1>Quiz</h1>
        <input v-model.trim="search" type="text" placeholder="Search..." />
      </header>
      <div class="options-container">
        <transition-group
          name="card"
          appear
          @before-enter="beforeEnter"
          @after-enter="afterEnter"
          @enter="enter"
        >
          <Card
            v-for="(quiz, index) in quizes"
            :key="quiz.id"
            :quiz="quiz"
            :data-index="index"
          />
        </transition-group>
      </div>
    </div>
  </main>
</template>

<style scoped>
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
  .card-enter-from {
    transform: translateY(-100px);
    opacity: 0;
  }
  .card-enter-to {
    opacity: 1;
    transform: translateY(0);
  }
  .card-enter-active {
    transition: all 0.4s ease-in-out;
  }
</style>
