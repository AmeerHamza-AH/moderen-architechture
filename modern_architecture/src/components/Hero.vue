<template>
  <div class="hero">
    <transition name="bg__left">
      <span class="bg bg__left" :key="bgNum" :data-number="bgNum">001</span>
    </transition>
    <transition name="bg__right">
      <span class="bg bg__right" :key="bgNum" :style="image"></span>
    </transition>
    <div class="left">
      <div class="top">
        <h3 class="text">good<br />mornign</h3>
        <div class="buttons">
          <button class="prev" @click="changeBgPrev">
            <Icon icon="bx:bx-chevron-left" />
          </button>
          <button class="next" @click="changeBgNext">
            <Icon icon="bx:bx-chevron-right" />
          </button>
        </div>
      </div>
      <transition name="left__title">
        <h1 class="title" :key="bgNum" :data-number="bgNum">
          modern architecture
        </h1>
      </transition>
      <div class="links">
        <a href="#" class="link">offer</a>
        <a href="#" class="link">projects</a>
      </div>
      <div class="bottom">
        <transition name="preview">
          <span
            class="preview"
            :key="bgNum"
            :style="image"
            :data-number="bgNum"
          >
            <Icon class="arrow-down" icon="bi:arrow-down" />
          </span>
        </transition>
        <div class="dots">
          <span class="dot" :class="bgNum === '001' ? 'active' : ''"></span>
          <span class="dot" :class="bgNum === '002' ? 'active' : ''"></span>
          <span class="dot" :class="bgNum === '003' ? 'active' : ''"></span>
          <span class="dot" :class="bgNum === '004' ? 'active' : ''"></span>
        </div>
      </div>
    </div>
    <div class="right">
      <button class="play">
        <Icon icon="ci:play-arrow" />
      </button>

      <div class="bottom">
        <div class="text">
          <h2 class="title">Some<br />centre</h2>
          <h4 class="city">Hong Kong</h4>
          <h4 class="date">January 20, 2019</h4>
        </div>
        <button class="enter">
          <Icon class="arrow-right" icon="bi:arrow-right" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Icon } from '@iconify/vue';
import { ref, computed } from 'vue';

const bgNum = ref('001');

const nums = ref(['001', '002', '003', '004']);

function changeBgPrev() {
  const idx = nums.value.indexOf(bgNum.value);
  if (idx === 0) {
    bgNum.value = nums.value[nums.value.length - 1];
    return;
  }
  bgNum.value = nums.value[idx - 1];
}

function changeBgNext() {
  const idx = nums.value.indexOf(bgNum.value);
  if (idx === nums.value.length - 1) {
    bgNum.value = nums.value[0];
    return;
  }
  bgNum.value = nums.value[idx + 1];
}

const image = computed(() => {
  return { backgroundImage: `url(./src/assets/${bgNum.value}.jpg)` };
});
</script>

<style scoped>
.hero {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.bg {
  position: absolute;
  z-index: -1;
}
.bg__left {
  top: 0;
  left: -40%;
  width: 100%;
  height: 100%;
  transform: skewX(-20deg) translateY(0);
}
.bg__left::after {
  content: attr(data-number);
  position: absolute;
  top: 50%;
  right: 0;
  font-size: 35rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: skewX(20deg) translateY(-50%);
  opacity: 0.04;
}

.bg__left-enter-from {
  transform: translate(-20%, 100%);
}
.bg__left-leave-to {
  transform: translate(20%, -100%);
}
.bg__left-enter-active,
.bg__left-leave-active {
  transition: 1s ease-in-out;
}

.bg__right {
  top: 0;
  right: -40%;
  width: 80%;
  height: 100%;
  transform: skewX(-20deg);
  background-image: url(../assets/001.jpg);
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  box-shadow: inset 0 0 20px #000;
}

.bg__right-enter-from {
  right: -24%;
  transform: skewX(-20deg) translate(20%, -100%);
}
.bg__right-leave-to {
  right: -56%;
  transform: skewX(-20deg) translate(-20%, 100%);
}
.bg__right-enter-active,
.bg__right-leave-active {
  transition: 1s ease-in-out;
}

.left {
  width: 400px;
}

.left .top {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5rem;
}

.left .top .text {
  text-transform: uppercase;
  font-weight: 300;
  font-size: 1rem;
}
.left .top .buttons {
  display: flex;
  gap: 1.5rem;
}
.left .top .buttons .prev,
.left .top .buttons .next {
  font-size: 1.6rem;
}
.left .title {
  position: relative;
  font-size: 4rem;
  font-weight: 400;
  text-transform: uppercase;
  margin-bottom: 5rem;
}
.left .title::after {
  position: absolute;
  top: 2rem;
  left: -6rem;
  content: attr(data-number);
  font-weight: 700;
  font-size: 0.8rem;
  opacity: 0.7;
}

.left__title-enter-from {
  opacity: 0;
}
.left__title-leave-to {
  opacity: 0;
}

.left__title-enter-active {
  transition: 1s ease-in-out;
}
.left__title-leave-active {
  display: none;
}

.left .links {
  display: flex;
  flex-direction: column;
}
.left .links .link {
  color: inherit;
  text-transform: uppercase;
}

.left .bottom {
  position: absolute;
  bottom: 4rem;
  display: flex;
  justify-content: flex-start;
  gap: 10rem;
  width: 400px;
  height: 80px;
}
.left .preview {
  position: absolute;
  display: block;
  top: 0;
  left: 0;
  width: 200px;
  height: 80px;
  background-image: url(../assets/001.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
.left .preview::before {
  content: attr(data-number);
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #fff;
  font-size: 1.4rem;
  text-shadow: 0 0 5px #000;
}
.left .preview .arrow-down {
  position: absolute;
  top: 0;
  left: -6rem;
  font-size: 2rem;
}

.preview-enter-from {
  transform: translate(-20%, 200%);
}

.preview-leave-to {
  transform: translate(-20%, 200%);
}
.preview-enter-active {
  transition: 0.4s 0.6s ease-in-out;
}
.preview-leave-active {
  transition: 0.5s ease-in-out;
}

.left .dots {
  position: absolute;
  right: 4rem;
  display: flex;
  gap: 1rem;
}
.left .dots .dot {
  display: block;
  width: 3px;
  height: 3px;
  background-color: #000;
  border-radius: 100%;
  transition: 1s ease-in-out;
}
.left .dots .dot:not(.active) {
  opacity: 0.4;
}

.left .dots .dot.active {
  transition: 1s ease-in-out;
}

.right {
  width: 400px;
  height: 100%;
  padding-bottom: 4rem;
  color: #fff;
  display: flex;
  flex-direction: column;
  gap: 14rem;
  align-items: flex-end;
  justify-content: flex-end;
}

.right .play {
  width: 40px;
  height: 40px;
  border: 1px solid #fff;
  box-shadow: 0 0 1px #fff;
  border-radius: 100%;
  margin-right: 0.5rem;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
}

.right .bottom {
  display: flex;
  gap: 10rem;
}

.right .title {
  font-size: 2rem;
  font-weight: 300;
  text-transform: uppercase;
  margin-bottom: 4rem;
}

.right .city,
.right .date {
  font-weight: 400;
  font-size: 1rem;
}

.right .enter {
  width: 50px;
  height: 120px;
  background-color: #fff;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  padding-bottom: 1.2rem;
}

.arrow-right {
  font-size: 2rem;
}
</style>
