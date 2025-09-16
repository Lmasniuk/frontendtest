<script setup>
defineProps({
  boardHistory: {
    type: Array,
    required: true,
  },
});
</script>
<template>
  <div class="history-wrapper">
    <h2>History</h2>
    <span> (oldest to newest)</span>
    <ul>
      <li v-for="previousMove in boardHistory">{{ previousMove }}</li>
    </ul>
  </div>
</template>
<style lang="scss" scoped>
li {
  list-style-type: none;
}

.history-wrapper {
  display: flex;
  flex-direction: column;
  width: 30%;
}
</style>
