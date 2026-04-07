<script setup lang="ts">

defineProps<{
  symbolCount: number
}>();

</script>

<template>
<div class="symbol__calc">Cимволов в минуту: {{ symbolCount }}</div>
</template>

<style scoped>
.symbol__calc {
  padding: 3px;
  width: auto;
  height: 20px;
  border: 1px solid black;
}
</style>