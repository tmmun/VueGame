<template>
  <div class="element_cont">
    <div id="but" class="but_short" @click="createCell()">start</div>
    <div id="but" class="but_short" @click="timerStop()">stop</div>

    <div
      id="timer"
      @click="level()"
      :class="timer < 26 ? 'timer_lost' : 'base_color'"
      v-if="timer != 0"
    >
      {{ timer }}
    </div>
    <div id="block" class="base_color" v-else>time</div>

    <div id="block" class="sum" v-if="sum != 0">
      {{ sum }}
    </div>
    <div id="block" class="sum" v-else>sum</div>

    <div
      id="block"
      :class="coin != 0 ? 'coin_add' : 'base_color'"
      v-if="coin != 0"
    >
      {{ coin }}
    </div>
    <div id="block" class="base_color" v-else>coin</div>
  </div>
</template>

<script>
export default {
  methods: {
    createCell() {
      this.$emit("createCell");
    },
    timerStop() {
      this.$emit("timerStop");
    },
    level() {
      this.$emit("level");
    },
  },
  props: {
    baseArr: Object,
    sum: Number,
    coin: Number,
    timer: Number,
  },
};
</script>

<style>

#timer {
  font-family: "Bebas Neue", cursive;
  width: var(--width-height);
  height: var(--width-height);
  margin: 5px 5px;
  text-align: center;
  line-height: var(--line-height);
  border-radius: 5px;
  font-size: 27px;
  cursor: pointer;
  user-select:none
}

#timer:active {
  line-height: 52px;
  color: #152534;
  background-color: var(--green-oll);
  border: solid;
  border-width: 3px 0px 0px;
  box-shadow: 0px 1px 0px #1e7044;
  height: 48px;
}

.coin_add {
  color: #71542f;
  background-color: #ffbd69;
  box-shadow: 0px 4px 0px #71542f;
}

.timer_lost {
  color: #71542f;
  background-color: #fb6b6c;
  box-shadow: 0px 4px 0px #bb5050;
}

.base_color {
  color: #182b3d;
  background-color: var(--green-oll);
  box-shadow: 0px 4px 0px #1e7044;
}

.sum {
  color: #132230;
  background-color: #254058;
  box-shadow: 0px 4px 0px #182b3d;
}
</style>