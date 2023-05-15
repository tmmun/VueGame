<template>
  <div>
    <div class="element_cont">
      <div class="text">add up the numbers and get</div>
      <div id="but" class="but_cell" @click="maxSumValUp()">{{ maxSumVal }}</div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    maxSumValUp() {
      this.$emit("maxSumValUp");
    },
  },
  props: {
    maxSumVal: Number,
  },
};
</script>

<style>
.text {
  font-family: "Bebas Neue", cursive;
  height: var(--width-height);
  width: 269px;
  margin: 5px 5px;
  text-align: center;
  line-height: var(--line-height);
  border-radius: 5px;
  font-size: 27px;
  color: #132230;
  background-color: #254058;
  box-shadow: 0px 4px 0px #182b3d;
  padding: 0px 10px;
}
.max_sum {
  background-color: var(--green-oll);
  box-shadow: 0px 4px 0px #1e7044;
  color: #182b3d;
}
</style>