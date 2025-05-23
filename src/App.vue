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

.todo-form {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 1.25rem;
}

.todo-input {
  flex-grow: 1;
  padding: 0.75rem;
  border: 2px solid #d1c4e9;
  border-radius: 0.75rem;
  font-size: 1rem;
  transition: border 0.3s ease;
}

.todo-input:focus {
  border-color: #7e57c2;
  outline: none;
}

.todo-button {
  background-color: #7e57c2;
  color: white;
  border: none;
  padding: 0.75rem 1.25rem;
  border-radius: 0.75rem;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.todo-button:hover {
  background-color: #5e35b1;
}

.filter-section {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin-bottom: 1rem;
  font-size: 0.95rem;
  color: #4a148c;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ede7f6;
  padding: 0.75rem 1rem;
  border-radius: 0.75rem;
  margin-bottom: 0.75rem;
  transition: background-color 0.3s ease;
}

.todo-item:hover {
  background-color: #d1c4e9;
}

.todo-text-wrapper {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.todo-text {
  color: #4a148c;
  font-size: 1rem;
}

.todo-text.completed {
  text-decoration: line-through;
  color: #9e9e9e;
  font-style: italic;
}

.delete-button {
  background: none;
  border: none;
  color: #e53935;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: bold;
  transition: color 0.3s ease;
}

.delete-button:hover {
  color: #b71c1c;
}

.clear-completed-section {
  text-align: center;
  margin-top: 1.5rem;
}

.clear-button {
  background-color: #ef5350;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 0.75rem;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.clear-button:hover {
  background-color: #c62828;
}
</style>
