<script setup>
  const { questionStatus, barPercentage } = defineProps([
    "questionStatus",
    "barPercentage",
  ]);
</script>
<template>
  <div>
    <header>
      <h4>Question {{ questionStatus }}</h4>
      <div class="bar">
        <div class="completion"></div>
      </div>
    </header>
  </div>
</template>

<style scoped>
  header {
    margin-top: 20px;
  }
  header h4 {
    font-size: 30px;
  }
  .bar {
    width: 300px;
    height: 50px;
    border: 3px solid
      linear-gradient(
        90deg,
        hsla(272, 76%, 68%, 1) 0%,
        hsla(319, 74%, 64%, 1) 100%
      );
  }
  .completion {
    height: 100%;
    width: v-bind(barPercentage);
    background: linear-gradient(
      90deg,
      hsla(272, 76%, 68%, 1) 0%,
      hsla(319, 74%, 64%, 1) 100%
    );
    transition: 0.8s ease-in all;
    animation: gradient 1s infinite ease;
  }
  @keyframes gradient {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }
</style>
