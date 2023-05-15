<template>
  <div>
    <global-info :maxSumVal="maxSumVal" @maxSumValUp="maxSumValUp" />
    <cell-hub :cells="baseArr.cells" @remove="deliteCell" />
    <counters
      :sum="baseArr.sum"
      :coin="baseArr.coin"
      :timer="baseArr.timer"
      v-on:createCell="createCell"
      v-on:timerStop="timerStop"
      v-on:level="level"
    />
  </div>
</template>

<script>
import CellHub from "./components/CellHub.vue";
import Counters from "./components/Counters.vue";
import GlobalInfo from "./components/GlobalInfo.vue";
export default {
  components: { CellHub, Counters, GlobalInfo },
  data() {
    return {
      baseArr: {
        cells: [],
        sum: 0,
        coin: 0,
        timer: 0,
        Interval: null,
        difficulty: [60, 40, 25],
      },
      timerTime: 60,
      sumNum: 0,
      diCo: 0,
      maxCellVal: 4,
      maxSumVal: 10,
    };
  },
  methods: {
    createCell() {
      if (this.baseArr.cells.length == 0) {
        for (let i = 0; i < 36; i++) {
          let newCell = Math.floor(Math.random() * this.maxCellVal) + 1;
          this.baseArr.cells.push(newCell);
        }
        this.baseArr.Interval = setInterval(this.incrSec, 1000);
      }
    },
    deliteCell(index) {
      this.baseArr.sum += this.baseArr.cells[index];

      if (this.baseArr.sum == this.maxSumVal) {
        this.baseArr.coin++;
        this.baseArr.sum = 0;
        localStorage.coin = this.baseArr.coin;
      }

      if (this.baseArr.sum > this.maxSumVal) {
        if (this.baseArr.coin > 0) {
          this.baseArr.coin--;
          localStorage.coin = this.baseArr.coin;
        }
        this.baseArr.sum = 0;
      }

      this.baseArr.cells.splice(index, 1);

      for (var i = 0; i < this.baseArr.cells.length; i++) {
        this.sumNum += this.baseArr.cells[i];
      }

      if (this.sumNum < this.maxSumVal) {
        this.baseArr.cells = [];
        this.baseArr.timer = this.timerTime;
        this.baseArr.sum = 0;
        clearInterval(this.baseArr.Interval);
      }

      this.sumNum = 0;

      if (this.baseArr.cells.length == 0) {
        this.baseArr.timer = this.timerTime;
        this.baseArr.sum = 0;
        clearInterval(this.baseArr.Interval);
      }
    },
    timerStop() {
      this.baseArr.cells = [];
      this.baseArr.timer = this.timerTime;
      this.baseArr.sum = 0;
      clearInterval(this.baseArr.Interval);
    },
    incrSec() {
      this.baseArr.timer--;

      if (this.baseArr.timer <= 0) {
        this.baseArr.cells = [];
        this.baseArr.sum = 0;
        this.baseArr.timer = this.timerTime;
        clearInterval(this.baseArr.Interval);
      }
    },
    level() {
      if (this.baseArr.cells.length == 0) {
        if (this.diCo < this.baseArr.difficulty.length - 1) {
          this.diCo++;
          this.baseArr.timer = this.baseArr.difficulty[this.diCo];
        } else {
          this.baseArr.timer = this.baseArr.difficulty[(this.diCo = 0)];
        }
      }
    },
    maxSumValUp() {
      if (this.baseArr.cells.length == 0){
        if (this.maxSumVal < 40) {
        this.maxCellVal += this.maxCellVal;
        this.maxSumVal += this.maxSumVal;
      } else {
        this.maxCellVal = 10
        this.maxSumVal = 10
      }
      }
    },
  },
  mounted() {
    this.baseArr.timer = this.timerTime;

    if (localStorage.coin) {
      this.baseArr.coin = Number(localStorage.coin);
    }
  },
};
</script>

<style>
:root {
  --width-height: 50px;
  --line-height: 53px;
  --green-oll: #2dad69;
}

.back {
  background-color: #182b3d;
}

#block {
  font-family: "Bebas Neue", cursive;
  width: var(--width-height);
  height: var(--width-height);
  margin: 5px 5px;
  text-align: center;
  line-height: var(--line-height);
  border-radius: 5px;
  font-size: 27px;
}

#but {
  font-family: "Bebas Neue", cursive;
  color: #182b3d;
  height: var(--width-height);
  background-color: var(--green-oll);
  margin: 5px 5px;
  text-align: center;
  line-height: var(--line-height);
  border-radius: 5px;
  font-size: 27px;
  box-shadow: 0px 4px 0px #1e7044;
  cursor: pointer;
  user-select:none
}

#but:active {
  line-height: 52px;
  color: #152534;
  background-color: var(--green-oll);
  border: solid;
  border-width: 3px 0px 0px;
  box-shadow: 0px 1px 0px #1e7044;
  height: 48px;
}

.but_cell {
  width: 50px;
}

.but_short {
  width: 79px;
}

.element_cont {
  margin-top: 15px;
  margin-bottom: 15px;
  margin-right: auto;
  margin-left: auto;
  padding: 5px 5px;
  border-radius: 10px;
  background-color: #11202e;
  width: 360px;
  height: 60px;
  display: flex;
  flex-wrap: wrap;
  align-content: flex-start;
  box-shadow: 0px 7px 0px #0d1823;
}
</style>