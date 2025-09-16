<script setup>
defineProps({
  boardHistory: {
    type: Array,
    required: true,
  },
});
</script>
<template>
  <div class="history">
    <div class="history__card">
      <h2>History</h2>
      <ul>
        <li v-for="(previousMove, index) in boardHistory">
          {{ index + 1 }}. {{ previousMove }}
        </li>
      </ul>
    </div>
  </div>
</template>
<style lang="scss" scoped>
li {
  list-style-type: none;
}

.history {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;

  @include desktop {
    width: 30%;
  }

  h2 {
    text-align: center;
  }

  &__card {
    padding: 1rem;
    background-color: rgb(130, 141, 127);
    border-radius: 1rem;
    width: 50%;
    margin-top: 2rem;
  }
}
</style>
