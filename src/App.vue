<script setup>
import { ref, computed } from 'vue'

const newTodo = ref('')
const todos = ref([])
const filter = ref('all')

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({ text: newTodo.value.trim(), completed: false })
    newTodo.value = ''
  }
}

const deleteTodo = (todoToDelete) => {
  const index = todos.value.indexOf(todoToDelete)
  if (index !== -1) {
    todos.value.splice(index, 1)
  }
}

const clearCompleted = () => {
  todos.value = todos.value.filter(todo => !todo.completed)
}

const filteredTodos = computed(() => {
  if (filter.value === 'complete') {
    return todos.value.filter(todo => todo.completed)
  } else if (filter.value === 'incomplete') {
    return todos.value.filter(todo => !todo.completed)
  }
  return todos.value
})
</script>

<template>
  <div class="app-container">
    <div class="todo-container">
      <h1 class="title">To-Do List</h1>

      <form @submit.prevent="addTodo" class="todo-form">
        <input v-model="newTodo" type="text" placeholder="Tambahkan kegiatan..." class="todo-input">
        <button type="submit" class="todo-button">Tambah</button>
      </form>

      <div class="filter-section">
        <label>
          <input type="radio" value="all" v-model="filter"> Semua
        </label>
        <label>
          <input type="radio" value="incomplete" v-model="filter"> Belum Selesai
        </label>
        <label>
          <input type="radio" value="complete" v-model="filter"> Selesai
        </label>
      </div>

      <ul class="todo-list">
        <li v-for="(todo, index) in filteredTodos" :key="index" class="todo-item">
          <div class="todo-text-wrapper">
            <input type="checkbox" v-model="todo.completed">
            <span :class="{'completed': todo.completed}" class="todo-text">{{ todo.text }}</span>
          </div>
          <button @click="deleteTodo(todo)" class="delete-button">Hapus</button>
        </li>
      </ul>

      <div class="clear-completed-section">
        <button @click="clearCompleted" class="clear-button">Hapus Semua yang Selesai</button>
      </div>
    </div>
  </div>
</template>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  background: linear-gradient(135deg, #f6f9ff, #eae6ff);
  min-height: 100vh;
}

.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
}

.todo-container {
  background-color: #ffffff;
  padding: 2rem;
  border-radius: 1.5rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 600px;
  transition: box-shadow 0.3s ease;
}

.todo-container:hover {
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.title {
  text-align: center;
  color: #4a148c;
  margin-bottom: 1.5rem;
  font-size: 2rem;
  font-weight: bold;
}
</style>
