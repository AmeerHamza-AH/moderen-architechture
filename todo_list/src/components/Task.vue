<template>
  <div class="task" :class="isDone">
    <span class="icon" @click="toggleDone"></span>
    <div class="task-data">
      <h1 class="title">{{ task.title }}</h1>
    </div>
    <button class="delete" @click="deleteTask">
      <Icon icon="bi:x-square" />
    </button>
  </div>
</template>

<script setup>
import { Icon } from '@iconify/vue';
import { ref, computed } from 'vue';

const props = defineProps({
  task: Object,
});

const localTask = ref(props.task);

const emit = defineEmits('is-done', 'delete-task-id');

function toggleDone() {
  localTask.value.done = !localTask.value.done;
  emit('is-done', {
    id: localTask.value.id,
    done: localTask.value.done,
  });
}

function deleteTask() {
  const id = props.task.id;
  emit('delete-task-id', id);
}

const isDone = computed(() => {
  if (localTask.value.done) return 'done';
});
</script>

<style scoped>
.task {
  display: flex;
  gap: 10px;
  align-items: center;
  height: 40px;
}

.icon {
  position: relative;
  display: block;
  width: 40px;
  height: 40px;
  cursor: pointer;
}

.icon::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 0;
  width: 30px;
  height: 3px;
  border-radius: 100px;
  background-color: var(--color-light-blue);
  transform: translateY(-50%);
  transition: 0.5s ease-in-out;
}

.icon::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  border-radius: 100px;
  background-color: var(--color-light-blue);
  transform: translate(-50%, -50%);
  transition: 0.5s ease-in-out;
}

.task.done .icon::before {
  top: 62%;
  height: 3px;
  width: 15px;
  transform: rotate(45deg);
}

.task.done .icon::after {
  top: 50%;
  left: 7px;
  height: 3px;
  width: 30px;
  transform: rotate(-45deg);
}

.title {
  position: relative;
  font-size: 16px;
  font-weight: 400;
  mix-blend-mode: difference;
  transition: 0.5s ease-in-out;
  height: inherit;
}

.title::after {
  content: '';
  position: absolute;
  top: 55%;
  left: -5px;
  transition: 0.5s ease-in-out;
  width: 0;
  height: 1px;
  background-color: var(--color-gray);
  transition: 0.5s ease-in-out;
}

.task.done .title {
  color: var(--color-gray);
  mix-blend-mode: difference;
  opacity: 0.5;
  transition: 0.5s ease-in-out;
}

.task.done .title::after {
  content: '';
  position: absolute;
  top: 55%;
  left: -5px;
  width: calc(100% + 10px);
  height: 1px;
  background-color: var(--color-gray);
}

.delete {
  background: none;
  outline: none;
  border: none;
  cursor: pointer;
  color: red;
  mix-blend-mode: hard-light;
  display: flex;
  align-items: center;
  margin-left: 5px;
  font-size: 16px;
}
</style>
