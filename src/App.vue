<template>
  <div class="header">
    <img src="/src/assets/notes_icon.png" alt="gambar" class="gambar">
    <h1>TO DO APP-DINDA</h1>
    <img src="/src/assets/notes_icon.png" alt="gambar" class="gambar">
  </div>
  
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="ketik disini">
    <button class="bnAdd-hover bnTodo">Tambah To do</button>
  </form>

  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
      <button @click="editTodo(todo)">Edit</button>
    </li>
  </ul>

    <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Semua' : 'Belum Selesai' }}
    </button>
  

</template>

<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Ubah format laporan', done: true },
  { id: id++, text: 'Kumpulkan tugas praktikum', done: false },
  { id: id++, text: 'Cek kuota internet', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

function editTodo(todo) {
  const newText = prompt('Edit todo:', todo.text)
  if (newText !== null) {
    todo.text = newText
  }
}
</script>

<style>
.header{
  display: flex;
  align-items: center; 
  margin-bottom: 20px; 
}

.done {
  text-decoration: line-through;
}

body {
  font-family: Arial, sans-serif;
  background-color: #ffd7c6; 
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: auto;
}

h1 {
  font-size: 35px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px; 
  color: #fd7236; 
}

.gambar{
  width: 50px; 
  height: 50px; 
  margin-left: 10px;
}

.container {
  max-width: 600px;
  width: 100%;
  padding: 20px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

form {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  justify-content: center; 
}

input[type="text"] {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 5px; 
}

button {
  padding: 8px 16px;
  background-color: #ff9466; 
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 5px; 
}

button:hover {
  background-color: #ff9466; 
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

span {
  flex: 1;
  margin-left: 10px;
}

.bottom-button {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}

.bnAdd-hover {
  width: auto;
  font-size: 15px;
  font-weight: 500;
  color: #fff;
  cursor: pointer;
  margin: 20px;
  height: auto;
  text-align:center;
  border: none;
  background-size: 300% 100%;
  border-radius: 50px;
  transition: all .4s ease-in-out;
}

.bnAdd-hover:hover {
  background-position: 100% 0;
  transition: all .4s ease-in-out;
}

.bnAdd-hover:focus {
  outline: none;
}

.bnAdd-hover.bnTodo {
  background-image: linear-gradient(
    to right,
    #e85a19,
    #ff9466,
    #ff9466,
    #f5ce62
  );
  box-shadow: 0 4px 15px 0 rgba(229, 66, 10, 0.75);
}

</style>