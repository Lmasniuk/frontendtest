<script setup>
import { ref } from "vue";

import HelloWorld from "./components/HelloWorld.vue";
import Chessboard from "./components/Chessboard.vue";

const boardHistory = ref([]);
</script>

<template>
  <HelloWorld msg="Vite + Vue" />
  <Chessboard :boardHistory="boardHistory" />
</template>

<style scoped></style>
