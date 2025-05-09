<script setup>
import { ref, computed } from 'vue'

</script>

<template>
      <form @submit.prevent="addTodo" class="todo-form">
        <input v-model="newTodo" type="text" placeholder="Tambahkan kegiatan..." class="todo-input">
        <button type="submit" class="todo-button">Tambah</button>
      </form>
</template>

<style scoped>

</style>
