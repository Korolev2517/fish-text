<script setup lang="ts">
import InputTextComp from "./components/InputTextComp.vue";
import SymbolCalcComp from "./components/SymbolCalcComp.vue";
import { ref } from "vue";

const textData = ref<string>('');
const totalTypedChars = ref<number>(0);

const handleTotalCharsUpdate = (value: number) => {
  totalTypedChars.value = value;
}

async function getText() {
  try {
    const response = await fetch('https://fish-text.ru/get?type=4')
    if (!response.ok) {
      throw new Error(`'Произошла ошибка: ', ${response.status}`)
    }
    const data = await response.json()
    textData.value = data.text;
} catch (err: any) {
    console.log('Произошла ошибка', err.message)
  } finally {
    console.log('Запрос завершен')
  }
}
getText();
</script>

<template>
  <div class="container">
    <SymbolCalcComp :symbolCount="totalTypedChars"/>
    <div class="response__text">
      <p>{{ textData }}</p>
    </div>
      <InputTextComp @updateTotalChars="handleTotalCharsUpdate"/>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  margin: 0;
  justify-content: center;
  align-items: center;
  gap: 2px;
}

.response__text {
  padding: 10px;
  width: 700px;
  height: 210px;
  border: 1px solid black;
}

.response__text p {
  margin: 0;
  font-size: 19px;
  line-height: 120%;
}
</style>
