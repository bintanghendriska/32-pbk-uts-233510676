<script setup>
import { ref, computed } from 'vue'

const newTodo = ref('')
const todos = ref([])


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
</script>

<template>
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
</template>

<style scoped>

</style>
