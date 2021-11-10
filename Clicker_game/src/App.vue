<script setup>
import { ref } from "vue";

let score = ref(0);
let addSize = ref(1);
let perSecond = ref(0);
let totalClicks = ref(0);
let clickUpdateCost = ref(10);
let secondUpdateCost = ref(20);
let interval = null;

function addToScore() {
  score.value += addSize.value;
  totalClicks.value++;
}

function increaseAddSize() {
  if (score.value >= clickUpdateCost.value) {
    score.value -= clickUpdateCost.value;
    addSize.value++;
    clickUpdateCost.value = parseInt(clickUpdateCost.value * 1.75);
  }
}

function startInterval() {
  interval = setInterval(() => {
    score.value += perSecond.value;
  }, 1000);
}

function increasePerSecond() {
  if (score.value >= secondUpdateCost.value) {
    clearInterval(interval);
    perSecond.value++;
    score.value -= secondUpdateCost.value;
    secondUpdateCost.value = parseInt(secondUpdateCost.value * 2.15);

    if (perSecond.value > 0) {
      startInterval();
    }
  }
}
</script>

<template>
  <div id="app" v-cloak>
    <div class="container">
      <div class="stats">
        <span class="clicks">Total Clicks: {{ score }}</span>
        <span class="perSecond">Per Second: {{ perSecond }}</span>
      </div>

      <div class="score">{{ score }}</div>

      <button class="btn-add" @click="addToScore">CLICK + {{ addSize }}</button>

      <div class="shop">
        <button class="btn-buy" @click="increaseAddSize">+1 on click</button>
        <span>Cost: {{ clickUpdateCost }}</span>
        <button class="btn-buy" @click="increasePerSecond">
          +1 per second
        </button>
        <span>Cost: {{ secondUpdateCost }}</span>
      </div>
    </div>
  </div>
</template>

<style>
html {
  box-sizing: border-box;
}

* {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app {
  font-family: sans-serif;
  font-size: 30px;
  font-weight: 700;
  color: #181818;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  min-width: 400px;
  border: 1px solid #cfcfcf;
  border-radius: 10px;
  padding: 20px;
  overflow: hidden;
}

.container::after {
  position: absolute;
  top: 40%;
  left: 50%;
  content: "";
  transform: translateX(-50%);
  width: 400%;
  height: 200%;
  box-shadow: 0 0 30px #cfcfcf;
  border-radius: 100%;
  z-index: -1;
}

.stats {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
  margin-bottom: 50px;
}

.stats span {
  font-size: 15px;
}

.score {
  font-size: 60px;
  margin-bottom: 50px;
}

.btn-add {
  width: 200px;
  height: 80px;
  border: 1px solid #999;
  border-radius: 5px;
  outline: none;
  box-shadow: 0 6px 16px #777;
  font-size: 22px;
  font-weight: 700;
  margin-bottom: 50px;
  background: linear-gradient(-35deg, #eee, #ccc);
  cursor: pointer;
}

.btn-add:hover {
  background: linear-gradient(-35deg, #eee, #bbb);
}

.btn-add:active {
  background: linear-gradient(-35deg, #eee, #bbb);
  box-shadow: 0 3px 4px #777;
  margin-top: 6px;
  margin-bottom: 44px;
}

.shop {
  display: grid;
  align-items: center;
  justify-content: center;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  row-gap: 10px;
  column-gap: 20px;
  font-size: 24px;
  font-weight: 700;
  margin-bottom: 10px;
}

.btn-buy {
  width: 130px;
  height: 50px;
  font-size: 16px;
  font-weight: 700;
  border: 1px solid #d5d5d5;
  border-radius: 5px;
  background: linear-gradient(125deg, #d5d5d5, #f5f5f5);
  cursor: pointer;
}

.btn-buy:hover {
  background: linear-gradient(125deg, #ddd, #fff);
}

.btn-buy:active {
  background: linear-gradient(125deg, #d5d5d5, #f5f5f5);
  box-shadow: inset 0 2px 3px #666;
}
</style>
