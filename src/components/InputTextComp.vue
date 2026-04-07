<script setup lang="ts">
import { ref, defineEmits } from "vue";

const inputData = ref<string>('');
const totalTypedChars = ref<number>(0);
const previousLength = ref<number>(0);

const emit = defineEmits(['updateTotalChars']);

const handleTextInput = (event: Event) => {
  const target = event.target as HTMLTextAreaElement;
  const newValue = target.value;
  const newLength = newValue.length;

  if (newLength > previousLength.value) {
    const addedChars = newLength - previousLength.value;
    totalTypedChars.value += addedChars;
  }

  previousLength.value = newLength;
  inputData.value = newValue;

  emit('updateTotalChars', totalTypedChars.value)
}
</script>

<template>
  <div class="input__text">
    <textarea
        :value="inputData"
        @input="handleTextInput"
    ></textarea>
  </div>
</template>

<style scoped>
.input__text {
  padding: 10px;
  width: 700px;
  height: 210px;
  border: 1px solid black;
 }

.input__text textarea {
  padding: 0;
  width: 100%;
  height: 100%;
  border: none;
  resize: none;
  appearance: none;
  outline: none;
  font: inherit;
  margin: 0;
  font-size: 19px;
  line-height: 120%;
}
</style>