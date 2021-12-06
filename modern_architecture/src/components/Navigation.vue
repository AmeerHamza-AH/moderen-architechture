<template>
  <div class="nav">
    <button class="burger" @click="open = !open">
      <transition-group name="burger">
        <Icon icon="ci:menu-alt-05" v-if="open" />
        <Icon icon="dashicons:menu" v-else />
      </transition-group>
    </button>

    <ul class="menu">
      <li class="menu__item">
        <a class="menu__link" href="#">offer</a>
      </li>
      <li class="menu__item">
        <a class="menu__link" href="#">work</a>
      </li>
      <li class="menu__item">
        <a class="menu__link" href="#">about</a>
      </li>
      <li class="menu__item">
        <a class="menu__link" href="#">contact</a>
      </li>
    </ul>

    <button class="language">english</button>
  </div>
</template>

<script setup>
import { Icon } from '@iconify/vue';
import { ref } from 'vue';

const open = ref(false);
</script>

<style scoped>
.nav {
  position: absolute;
  top: 4rem;
  left: 0;
  width: 100%;
  padding: 0 8rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1.2rem;
  z-index: 10;
}

.burger {
  font-size: 3rem;
  width: 3rem;
  height: 3rem;
}

.burger-enter-from {
  opacity: 0;
}
.burger-leave-to {
  opacity: 0;
}
.burger-enter-active {
  transition: 0.5s 0.5s ease-in-out;
}
.burger-leave-active {
  transition: 0.5s ease-in-out;
}
.menu {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  text-transform: uppercase;
}

.menu__link {
  position: relative;
  text-decoration: none;
  color: inherit;
}
.menu__link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 1px;
  background-color: #000;
  transition: 0.5s ease-in-out;
}
.menu__link:hover::after {
  width: 100%;
}

.language {
  font-family: Outfit, sans-serif;
  text-transform: uppercase;
  font-size: 1.2rem;
  color: #fff;
  text-shadow: 0 0 4px #000;
  font-weight: 600;
}
</style>
