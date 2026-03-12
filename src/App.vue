<template>
  <div class="container">
    <h2>Task 3</h2>

    <div class="form">
      <input
        v-model="newTitle"
        type="text"
        placeholder="Назва продукту"
      />
      <select v-model="newCategory">
        <option value="Fruit">Fruit</option>
        <option value="Vegetable">Vegetable</option>
        <option value="Other">Other</option>
      </select>
      <button @click="addProduct">Додати продукт</button>
    </div>

    <button @click="clearProducts">Очистити список</button>

    <ul>
      <li
        v-for="p in products"
        :key="p.id"
        :class="{ highlighted: p.category === 'Fruit' }"
      >
        <strong>{{ p.title }}</strong> — {{ p.category }}
        <button @click="removeProduct(p.id)">Видалити</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const products = ref([
      { id: 1, title: 'Apple', category: 'Fruit' },
      { id: 2, title: 'Carrot', category: 'Vegetable' },
      { id: 3, title: 'Banana', category: 'Fruit' }
    ])

    const newTitle = ref('')
    const newCategory = ref('Fruit')

    const addProduct = () => {
      if (!newTitle.value.trim()) return 
      const newId = products.value.length
        ? Math.max(...products.value.map(p => p.id)) + 1
        : 1
      products.value.push({
        id: newId,
        title: newTitle.value,
        category: newCategory.value
      })
      newTitle.value = '' 
      newCategory.value = 'Fruit' 
    }

    const removeProduct = (id) => {
      products.value = products.value.filter(p => p.id !== id)
    }

    const clearProducts = () => {
      products.value = []
    }

    return {
      products,
      newTitle,
      newCategory,
      addProduct,
      removeProduct,
      clearProducts
    }
  }
}
</script>

<style>
.container {
  font-family: Arial, sans-serif;
  padding: 20px;
}

.form {
  margin-bottom: 10px;
}

input, select {
  padding: 5px;
  margin-right: 5px;
}

button {
  padding: 6px 12px;
  margin: 2px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 5px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.highlighted {
  background-color: rgb(215, 244, 254);
}
</style>