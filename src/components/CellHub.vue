<template>
  <div class="fon">
    <div
      class="cell"
      v-for="(cell, index) in cells"
      :key="cell"
      @click="$emit('remove', index)"
    >
      {{ cell }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    baseArr: Object,
    cells: Array,
  },
};
</script>

<style>
.cell {
  font-family: "Bebas Neue", cursive;
  color: #182b3d;
  width: var(--width-height);
  height: var(--width-height);
  background-color: var(--green-oll);
  margin: 5px 5px;
  text-align: center;
  line-height: var(--line-height);
  border-radius: 5px;
  font-size: 27px;
  box-shadow: 0px 4px 0px #1e7044;
}
.cell:active {
  line-height: 52px;
  color: #152534;
  background-color: var(--green-oll);
  border: solid;
  border-width: 3px 0px 0px;
  box-shadow: 0px 1px 0px #1e7044;
  height: 48px;
}
.fon {
  margin-right: auto;
  margin-left: auto;
  padding: 5px 5px;
  border-radius: 10px;
  background-color: #11202e;
  width: 360px;
  height: 360px;
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  box-shadow: 0px 7px 0px #0d1823;
}
</style>