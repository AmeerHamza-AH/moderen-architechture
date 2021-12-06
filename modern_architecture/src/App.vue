<template>
  <navigation></navigation>
  <hero></hero>
</template>

<script setup>
import Navigation from './components/Navigation.vue';
import Hero from './components/Hero.vue';
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Outfit:100,200,300,regular,500,600,700,800,900);

html {
  box-sizing: border-box;
  font-size: 10px;
}

*,
*::before,
*::after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}

body {
  height: 100vh;
  font-family: Outfit, Arial, sans-serif;
  overflow: hidden;
}

ul {
  list-style: none;
}

button {
  border: none;
  outline: none;
  background: none;
  cursor: pointer;
  font-family: Outfit, Arial, sans-serif;
}

#app {
  width: 100%;
  height: 100%;
}
</style>
