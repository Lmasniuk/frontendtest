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
      <div class="history__title">
        <h2>History</h2>
      </div>
      <ul class="history__content">
        <li class="history__item" v-for="(previousMove, index) in boardHistory">
          {{ index + 1 }}.
          {{
            previousMove[0] + String.fromCharCode(Number(previousMove[1]) + 96)
          }}
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

  &__card {
    border: 1px solid #5c5c5c;
    border-radius: 0.5rem;
    width: 50%;
    max-height: 640px;
    overflow: scroll;
  }

  &__title {
    padding: 0.5rem 1rem;
    position: sticky;
    top: 0;
    left: 0;
    /* border-bottom: 1px solid #383838; */
  }

  &__content {
    color: #5c5c5c;
    padding: 0;
  }

  &__item {
    padding: 0.5rem 1rem;
    border-top: 1px solid #aeaeae;

    /* &:last-child {
      border-bottom: none;
    } */
  }
}
</style>
