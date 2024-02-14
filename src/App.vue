<template>
  <div class="title-container">
    <h1>🔥🔥🔥KALKULATOR 🔥🔥🔥</h1>
  </div>
  <div class="calculator">
    <input type="text" v-model="input" disabled>
    <div class="buttons">
      <div class="row" v-for="row in buttonRows" :key="row">
        <button class="button" v-for="button in row" :key="button.value" @click="handleButtonClick(button.value)">
          {{ button.label }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>

import { ref } from 'vue';


const input = ref('');

const buttonRows = [
  [{ label: '7', value: '7' }, { label: '8', value: '8' }, { label: '9', value: '9' }, { label: '+', value: '+' }],
  [{ label: '4', value: '4' }, { label: '5', value: '5' }, { label: '6', value: '6' }, { label: '-', value: '-' }],
  [{ label: '1', value: '1' }, { label: '2', value: '2' }, { label: '3', value: '3' }, { label: '*', value: '*' }],
  [{ label: 'C', value: 'clear' }, { label: '0', value: '0' }, { label: '=', value: 'equals' }, { label: '/', value: '/' }]
];

const handleButtonClick = (value) => {
  if (value === 'clear') {
    input.value = '';
  } else if (value === 'equals') {
    calculateResult();
  } else {
    input.value += value;
  }

};

const calculateResult = () => {
  try {
    input.value = eval(input.value);
  } catch (error) {
    input.value = 'Error';
    // Jika terjadi kesalahan, reset input
    setTimeout(() => {
      input.value = '';
    }, 1000);
  }
};

</script>



<style>

.title-container {
  font-family: "Roboto",sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: slateblue;
}

h1 {
  color: white;
}

.calculator {
  width: 300px;
  margin: 50px auto;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  background-color: slateblue;
}

.buttons {
  display: flex;
  flex-direction: column;
}

.row {
  display: flex;
}

.button {
  flex: 1;
  padding: 20px;
  font-size: 20px;
  border: 1px solid #ccc;
  background-color: #f0f0f0;
  font-family: "Roboto",sans-serif;
  color: black;
  cursor: pointer;
}

input {
  width: 92%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 24px;
  text-align: right;
}
</style>