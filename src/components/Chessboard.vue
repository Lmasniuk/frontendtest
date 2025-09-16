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

  // push to the parent's boardHistory
  const updatedHistory = [...props.modelValue, squarePosition];
  emit("update:modelValue", updatedHistory);
};
</script>

<template>
  <div class="board-wrapper">
    <h1>Chessboard</h1>

    <div class="board">
      <div
        v-for="square in squares"
        :key="square.row + square.col"
        class="square"
        :class="[
          (square.row + square.col) % 2 === 0 ? 'dark' : 'light',
          activeSquare === `${square.row}${square.col}` ? 'highlighted' : '',
        ]"
        @click="setActiveSquare(`${square.row}${square.col}`)"
      >
        {{ square.row }}{{ String.fromCharCode(96 + square.col) }}
      </div>
    </div>
    <p>Active Square: {{ activeSquare }}</p>
  </div>
</template>

<style lang="scss" scoped>
.board-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 70%;
}

.board {
  margin-left: auto;
  margin-right: auto;
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(8, 1fr);
  max-width: 640px;
}

.square {
  width: 80px;
  height: 80px;
  display: flex;
  align-items: flex-end;
  padding: 6px;
  border: 4px solid transparent;

  &.dark {
    background-color: $square-color-1;
  }
  &.light {
    background-color: $square-color-2;
  }

  &.highlighted {
    border: 4px solid yellow;
  }
}
</style>
