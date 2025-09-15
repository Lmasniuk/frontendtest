<script setup>
import { ref } from "vue";
import Chessboard from "./Chessboard.vue";

defineProps({
  msg: String,
});

const count = ref(0);
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
  </div>
  <Chessboard />
</template>

<style scoped></style>
