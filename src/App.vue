<script setup>
import { ref, watch } from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
let newTodo = ref('')
let filter = ref('all')
watch(todos, function (value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, { deep: true })

function todoFilter(todo) {
  if (filter.value == 'active') {
    return todo.complete == false;
  } else if (filter.value == 'completed') {
    return todo.complete == true;
  } else {
    return true
  }
}
function activeFilter(todo) {
  return todo.complete == false
}

function addTodo() {
  todos.value.push({
    text: newTodo.value,
    complete: false
  })

  newTodo.value = ""
}
function deleteTodo(index) {
  todos.value.splice(index, 1)
}
</script>

<template>
  <h1>My Todo Application</h1>
  <p>{{ todos.filter(activeFilter).length }} items left</p>
  <input id="newtodo" placeholder="Add new Todo" v-model="newTodo" @keydown.enter="addTodo">
  <button @click="addTodo"> Add Todo</button>
  <p v-if="todos.length > 0">

    <input name="filter" type="radio" value="all" v-model="filter">
    <label>All</label>

    <input name="filter" type="radio" value="active" v-model="filter">
    <label>Active</label>

    <input name="filter" type="radio" value="completed" v-model="filter">
    <label>Completed</label>


  </p>
  <ol>
    <li v-for="(todo, index) in todos.filter(todoFilter)">

      <input type="checkbox" v-model="todo.complete">
      <button @click="deleteTodo(index)">🚮</button>
      <span  :class="{ completed: todo.complete }">
        {{ todo.text }}  
      </span>
    </li>
  </ol>
</template>

<style>
body {
  background: rgb(88, 50, 108);
  background: linear-gradient(117deg, rgb(244, 194, 194) 0%, rgb(137, 207, 240) 100%);
  font-family: 'Bruno Ace SC', cursive;
  text-align: center;
  min-height: 100vh;
}

input[type="checkbox"] {
  appearance: none;
  -webkit-appearance: none;
  height: 20px;
  width: 20px;
  background-color: black;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

input[type="checkbox"]:after {
  font-family: "Font Awesome 5 Free";
  content: "\f00c";
  font-weight: 900;
  font-size: 20px;
  color: rgb(137, 207, 240);
  display: none 
}

input[type="checkbox"]:hover {
  background-color: rgb(137, 207, 240);
}

input[type="checkbox"]:checked {
  background-color: rgb(244, 194, 194);
  height: 20px;
  width: 20px;
}

input[type="checkbox"]:checked::after {
  display: block;
}

.completed {
  text-decoration: line-through;
  color: black;
}

li {
  padding: 12px; 
  box-shadow: 5px 10px purple;
  border: 1px solid;
}
</style>