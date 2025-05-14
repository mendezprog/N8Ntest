<template lang="pug">
.quiz-grid
  .question-row
    .question {{ questionData.text }}
  .options-row
    .option(
      v-for="(option, index) in optionsData"
      :key="index"
      @click="selectOption(option.value)"
      :class="{ 'selected': selectedOption === option.value }"
    )
      | {{ option.text }}
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface Option {
  text: string;
  value: any; // Puedes especificar un tipo más concreto si lo necesitas
}

const questionData = {
  text: '¿Cuál es tu lenguaje de programación favorito?',
  placeholder: 'pregunta-principal'
};

const optionsData = [
  { text: 'JavaScript', value: 'js-valor' },
  { text: 'Python', value: 'python-valor' },
  { text: 'Java', value: 'java-valor' },
];

const emit = defineEmits(['option-selected']);

const selectedOption = ref<any | null>(null);

const selectOption = (value: any) => {
  selectedOption.value = value;
  emit('option-selected', value);
};
</script>

<style scoped lang="scss">
.quiz-grid {
  display: grid;
  grid-template-rows: auto auto;
  gap: 16px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;

  .question-row {
    .question {
      font-size: 1.2rem;
      font-weight: bold;
      margin-bottom: 10px;
    }
  }

  .options-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;

    .option {
      padding: 12px;
      border: 1px solid #ddd;
      border-radius: 6px;
      text-align: center;
      cursor: pointer;
      transition: background-color 0.2s ease;

      &:hover {
        background-color: #f0f0f0;
      }

      &.selected {
        background-color: #e0e0e0;
      }
    }
  }
}
</style>