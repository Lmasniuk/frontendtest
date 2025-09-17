<script setup>
defineProps({
  boardHistory: {
    type: Array,
    required: true,
  },
});

const timeSince = (timestamp) => {
  const now = Date.now();
  const diffMs = now - timestamp;
  const diffSec = Math.floor(diffMs / 1000);

  if (diffSec < 60) {
    return `${diffSec} second${diffSec !== 1 ? "s" : ""} ago`;
  }

  const diffMin = Math.floor(diffSec / 60);
  if (diffMin < 60) {
    return `${diffMin} minute${diffMin !== 1 ? "s" : ""} ago`;
  }

  const diffHours = Math.floor(diffMin / 60);
  if (diffHours < 24) {
    return `${diffHours} hour${diffHours !== 1 ? "s" : ""} ago`;
  }

  const diffDays = Math.floor(diffHours / 24);
  return `${diffDays} day${diffDays !== 1 ? "s" : ""} ago`;
};
</script>
<template>
  <div class="history">
    <div class="history__title">
      <h1>History</h1>
    </div>
    <ul class="history__content">
      <li class="history__item" v-for="(previousMove, index) in boardHistory">
        <span>
          {{ index + 1 }}.
          {{
            previousMove.squarePosition[0] +
            String.fromCharCode(Number(previousMove.squarePosition[1]) + 96)
          }}
        </span>
        <span class="history__timestamp"
          >{{ timeSince(previousMove.date) }} ago</span
        >
      </li>
    </ul>
  </div>
</template>
<style lang="scss" scoped>
li {
  list-style-type: none;
}

.history {
  background-color: #ffffff;
  border-radius: 0.5rem;
  width: 100%;
  max-height: calc(
    100vh - (($square-size-mobile * 8) + 4rem)
  ); /* 4 rem added to accommodate padding of wrappers */
  overflow: scroll;

  @include desktop {
    width: 30%;
    max-height: calc(
      ($square-size-desktop * 8) + 4rem
    ); /* 4 rem added to accommodate padding of wrappers*/
  }

  &__title {
    padding: 1rem;
    font-size: 0.6rem;
    position: sticky;
    top: 0;
    left: 0;
    background-color: white;
  }

  &__content {
    padding: 1rem;
    color: #5c5c5c;
    padding: 0;
  }

  &__item {
    padding: 0.5rem 1rem;
    border-bottom: 1px solid #aeaeae;
    display: flex;
    justify-content: space-between;
    align-items: center;

    &:last-child {
      border-bottom: none;
    }
  }

  &__timestamp {
    font-size: 0.6rem;
  }
}
</style>
