<script setup>
import { ref } from "vue";
import Square from "./Square.vue";

defineProps({
  boardHistory: {
    type: Array,
    required: true,
  },
});

const activeSquare = ref("11");
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
};
</script>

<template>
  <div>
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
