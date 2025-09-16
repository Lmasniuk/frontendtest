<script setup>
import Chessboard from "./components/Chessboard.vue";
import Sidebar from "./components/Sidebar.vue";

const boardHistory = defineModel({ default: [] });
</script>

<template>
  <div class="wrapper">
    <Chessboard v-model="boardHistory" />
    <Sidebar :boardHistory="boardHistory" />
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  padding: 2rem;

  @include desktop {
    flex-direction: row;
  }
}
</style>
