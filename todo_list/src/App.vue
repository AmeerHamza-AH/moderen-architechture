<template>
  <div class="background"></div>

  <div class="header">
    <h1 class="title">ToDo {{ date }}</h1>

    <button class="btn-hide-completed" @click="toggleShowCompletedFlag">
      <transition name="hide-btn" mode="out-in">
        <span :key="hideText">{{ hideText }}</span>
      </transition>
      completed
    </button>
  </div>

  <div class="tasks" v-if="tasks.length > 0">
    <div class="tasks-wrapper">
      <transition-group name="show-hide">
        <task
          v-for="task in filteredTasks"
          :key="task"
          :task="task"
          @is-done="changeDoneStatus"
          @delete-task-id="deleteTask"
        ></task>
      </transition-group>
    </div>
  </div>
  <div v-else class="no-tasks">
    <h1 class="title">No tasks</h1>
  </div>

  <new-task @new-task="addTask"></new-task>
</template>

<script setup>
import Task from './components/Task.vue';
import NewTask from './components/NewTask.vue';
import { ref, computed } from 'vue';

const showCompletedFlag = ref(true);
const hideText = ref('Hide');

const tasks = ref([
  {
    id: 123123123,
    title: 'Task one',
    done: true,
  },
  {
    id: 12312312354,
    title: 'Task two',
    done: false,
  },
  {
    id: 89787495834,
    title: 'Task three',
    done: false,
  },
  {
    id: 32847928374,
    title: 'Task four',
    done: false,
  },
]);

function toggleShowCompletedFlag() {
  showCompletedFlag.value = !showCompletedFlag.value;
}

function changeDoneStatus(data) {
  let task = tasks.value.filter((item) => item.id === data.id);
  task.done = data.done;
}

function addTask(data) {
  tasks.value.unshift({
    id: Date.now(),
    title: data.title,
    done: false,
  });
}

function deleteTask(data) {
  const taskToDelete = tasks.value.find((el) => el.id === data);
  const idx = tasks.value.indexOf(taskToDelete);

  tasks.value.splice(idx, 1);
}

const filteredTasks = computed(() => {
  if (showCompletedFlag.value) {
    hideText.value = 'Hide';
    return tasks.value;
  }

  hideText.value = 'Show';
  return tasks.value.filter((task) => task.done === false);
});
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Roboto:100,100italic,300,300italic,regular,italic,500,500italic,700,700italic,900,900italic);

:root {
  --color-white: #fafafa;
  --color-blue: #1a1c29;
  --color-light-blue: #449dd5;
  --color-gray: #8f9297;
}

html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  padding: 0;
}

#app {
  font-family: Roboto, Arial, sans-serif;
  background-color: var(--color-blue);
  width: 100vw;
  height: 100vh;
  margin-top: 60px;
  margin: 0;
  padding: 0;
  color: var(--color-white);
  display: flex;
  flex-direction: column;
  justify-content: center;
  box-shadow: inset 0 0 10px #000;
}

.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: var(--color-white);
  clip-path: polygon(0 0, 100% 0, 100% 100%);
  box-shadow: inset 0 0 10px #000;
}

.header {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  max-width: 400px;
  width: 100vw;
  display: flex;
  flex-direction: column;
  mix-blend-mode: difference;
}

.header .title {
  margin-left: 15px;
  margin-top: 50px;
  margin-bottom: 10px;
  font-weight: 400;
}

.btn-hide-completed {
  align-self: flex-end;
  z-index: 100;
  border: none;
  background: none;
  color: var(--color-white);
  width: 120px;
  text-align: right;
  margin-right: 15px;
  font-weight: 500;
  cursor: pointer;
  transition: 0.5s ease-in-out;
}

.tasks {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: 1s ease-in-out;
}

.tasks-wrapper {
  display: flex;
  flex-direction: column;
  gap: 30px;
  height: auto;
  transition: 1s ease-in-out;
}

.show-hide-enter-from {
  opacity: 0;
}
.show-hide-leave-to {
  opacity: 0;
}
.show-hide-enter-active,
.show-hide-leave-active {
  transition: 0.5s ease-in-out;
}

.hide-btn-enter-from {
  opacity: 0;
}
.hide-btn-leave-to {
  opacity: 0;
}
.hide-btn-enter-active,
.hide-btn-leave-active {
  transition: 1s ease-in-out;
}

.no-tasks {
  display: flex;
  justify-content: center;
  mix-blend-mode: difference;
}

.no-tasks .title {
  font-weight: 400;
}
</style>
