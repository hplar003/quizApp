<script setup>
  const { question } = defineProps(["question"]);
  const emit = defineEmits(["selectOption"]);

  const emitSelectedOptions = (isCorrect) => {
    emit("selectOption", isCorrect);
  };
</script>
<template>
  <div>
    <div class="question-container">
      <h1 class="question">{{ question.text }}</h1>
    </div>
    <div
      v-for="opt in question.options"
      :key="opt.id"
      class="options-container"
      @click="emitSelectedOptions(opt.isCorrect)"
    >
      <div class="option">
        <p class="option-label">{{ opt.label }}</p>
        <div class="option-value">
          <p>{{ opt.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .question-container {
    margin-top: 20px;
  }
  .question {
    font-size: 40px;
    margin-bottom: 20px;
  }
  .option {
    display: flex;
    margin-bottom: 20px;
    cursor: pointer;
  }
  .option-label {
    width: 50px;
    height: 50px;
    font-size: 30px;
    background: rgb(136, 65, 230);
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
  }
  .option-value {
    background-color: rgb(219, 198, 246);
    width: 100%;
    font-size: 30px;
    padding: 0 20px;
  }
</style>
