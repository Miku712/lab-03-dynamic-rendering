<template>
  <div class="container">
    <h2>Task 2: v-if vs v-show</h2>

    <button @click="togglePanel">Показати / Сховати панель</button>

    <hr>

    <div v-if="isPanelVisible" class="panel">
      <p>Ця панель керується v-if</p>
    </div>

    <div v-show="isPanelVisible" class="panel">
      <p>Ця панель керується v-show</p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const isPanelVisible = ref(false)

    const togglePanel = () => {
      isPanelVisible.value = !isPanelVisible.value
    }

    return {
      isPanelVisible,
      togglePanel
    }
  }
}
</script>

<style>
.container {
  font-family: Arial, sans-serif;
  padding: 20px;
}

button {
  margin: 5px 0;
  padding: 6px 12px;
  background-color: rgb(179, 233, 251);
  border-width: 1px;
}

.panel {
  border: 1px solid #333;
  padding: 10px;
  margin: 10px 0;
  background-color: rgb(226, 248, 255);
}
</style>