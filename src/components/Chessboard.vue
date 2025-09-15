<template lang="">
  <div>
    <h1>Chessboard</h1>
    <div class="square1"></div>
    <div class="square2"></div>
  </div>
</template>
<script>
export default {};
</script>
<style lang="scss" scoped>
@import "../styles/_variables.scss";
.square1 {
  width: 100px;
  height: 100px;
  background-color: $square-color-1;
}

.square2 {
  width: 100px;
  height: 100px;
  background-color: $square-color-2;
}
</style>
