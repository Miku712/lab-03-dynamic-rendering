<template>
  <div class="container">
    <h2>Стан сторінки</h2>

    <div v-if="isLoading">
      Завантаження...
    </div>
    <div v-else-if="hasError">
      Помилка завантаження
    </div>
    <div v-else-if="items.length === 0">
      Немає даних
    </div>
    <ul v-else>
      <li v-for="item in items" :key="item.id">
        {{ item.name }}
      </li>
    </ul>

    <hr>

    <div class="buttons">
      <button @click="toggleLoading">Toggle loading</button>
      <button @click="toggleError">Toggle error</button>
      <button @click="clearItems">Clear items</button>
      <button @click="addItems">Add sample items</button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const isLoading = ref(false)
    const hasError = ref(false)
    const items = ref([])

    const toggleLoading = () => {
      isLoading.value = !isLoading.value
      if (isLoading.value) {
        hasError.value = false
      }
    }

    const toggleError = () => {
      hasError.value = !hasError.value
      if (hasError.value) {
        isLoading.value = false
      }
    }

    const clearItems = () => {
      items.value = []
    }

    const addItems = () => {
      items.value = [
        { id: 1, name: 'History' },
        { id: 2, name: 'Math' },
        { id: 3, name: 'English' },
      ]
    }

    return {
      isLoading,
      hasError,
      items,
      toggleLoading,
      toggleError,
      clearItems,
      addItems
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
  margin: 5px;
  padding: 6px 12px;
  background-color: rgb(179, 233, 251);
  border-width: 1px;
}
</style>