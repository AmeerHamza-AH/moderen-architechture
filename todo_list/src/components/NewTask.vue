<template>
  <form class="input-form" @submit.prevent="sendTask">
    <div class="input-task">
      <label class="plus" for="input-new-task">
        <Icon icon="akar-icons:plus" />
      </label>

      <input
        type="text"
        id="input-new-task"
        class="input-new-task"
        placeholder="Write new task..."
      />
    </div>
  </form>
</template>

<script setup>
import { Icon } from '@iconify/vue';

const emit = defineEmits('new-task');

function sendTask({ target }) {
  const title = target.children[0].children[1].value;
  emit('new-task', {
    title,
  });
  target.reset();
}
</script>

<style scoped>
.input-form {
  position: absolute;
  bottom: 0%;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 90%;
  align-self: center;
  margin-bottom: 50px;
}

.input-task {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.input-new-task {
  background: none;
  border: none;
  color: var(--color-gray);
  opacity: 0.5;
  align-self: center;
  cursor: pointer;
  height: 20px;
}

.input-new-task:focus-visible {
  outline: none;
}

.plus {
  height: 20px;
  color: var(--color-gray);
  opacity: 0.5;
  margin-right: 10px;
  cursor: pointer;
  display: flex;
  align-items: center;
}
</style>
