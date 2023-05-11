<script setup>
import {ref} from 'vue'
let todos = ref ([])
let newTodo = ref('')
function AddTodo(){
  todos.value.push(newTodo.value)

  newTodo.value =""
}
function deleteTodo(index){
  todos.value.splice(index,1)
}
</script>

<template>
   

  <h1>My Todo Application</h1>
<ol>
  <li v-for="(todo, index) in todos">
    <button @click="deleteTodo(index)">🚮</button>
    {{ todo }}
  </li>
</ol>

<input v-model="newTodo" @keydown.enter="AddTodo">
<button @click="AddTodo"> Add Todo</button>
</template>

<style>
body  {
    background: rgb(88,50,108);
background: linear-gradient(117deg, rgb(244, 194, 194) 0%, rgb(137,207,240) 100%);
font-family: 'Bruno Ace SC', cursive;
    text-align: center;
    min-height: 100vh;
}
</style>
