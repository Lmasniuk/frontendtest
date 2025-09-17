<script setup>
import { ref } from "vue";

const props = defineProps({
  modelValue: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["update:modelValue"]);

const activeSquare = ref("");
const rows = [8, 7, 6, 5, 4, 3, 2, 1];
const cols = [1, 2, 3, 4, 5, 6, 7, 8];

// const squares = rows.flatMap((r) => cols.map((c) => ({ row: r, col: c })));

const squares = rows.flatMap((row) => {
  return cols.map((col) => {
    return {
      row: row,
      col: col,
    };
  });
});

const setActiveSquare = (squarePosition) => {
  activeSquare.value = squarePosition;

  const boardHistoryEntry = {
    squarePosition,
    date: Date.now(),
  };

  const updatedHistory = [...props.modelValue, boardHistoryEntry];
  emit("update:modelValue", updatedHistory);
};
</script>

<template>
  <div class="board-wrapper">
    <div class="board">
      <div
        v-for="square in squares"
        :key="square.row + square.col"
        class="square"
        :class="[
          'square',
          (square.row + square.col) % 2 === 0 ? 'dark' : 'light',
          activeSquare === `${square.row}${square.col}` ? 'highlighted' : '',
        ]"
        @click="setActiveSquare(`${square.row}${square.col}`)"
      >
        {{ square.row }}{{ String.fromCharCode(96 + square.col) }}
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.board-wrapper {
  background-color: #ffffff;
  border-radius: 0.75rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  padding: 1rem;

  @include desktop {
    padding: 2rem;
  }
}

.board {
  margin-left: auto;
  margin-right: auto;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(8, 1fr);
  width: 100%;
  max-width: calc($square-size-mobile * 8);

  @include desktop {
    max-width: calc($square-size-desktop * 8);
  }
}

.square {
  width: $square-size-mobile;
  height: $square-size-mobile;
  display: flex;
  align-items: flex-end;
  border: 2px solid transparent;
  padding: 0.25rem;
  transition: border-color 0.3s ease;
  font-size: 0.7rem;
  @include desktop {
    width: $square-size-desktop;
    height: $square-size-desktop;
  }

  &.dark {
    background-color: $square-color-1;
  }
  &.light {
    background-color: $square-color-2;
  }

  &.highlighted {
    border: 2px solid $square-outline-color;
  }
}
</style>
