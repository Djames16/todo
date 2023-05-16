<script setup>
import {ref, watch} from 'vue'
let todos = ref (JSON.parse(window.localStorage.getItem('todos'))??[])
let newTodo = ref('')
watch(todos, function(value){
  window.localStorage.setItem('todos', JSON.stringify(value))
  }, {deep: true})
function AddTodo(){
  todos.value.push({
    text: newTodo.value,
    complete: false
  })

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
    <input type="checkbox" v-model="todo.complete">
    <button @click="deleteTodo(index)">🚮</button>
    <span :class="{completed: todo.complete}">
    {{ todo.text }}
    </span>
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

input[type="checkbox"]{
  appearance: none;
  -webkit-appearance: none;
  height: 20px;
  width:20px;
  background-color: black;
  cursor:pointer;
  display:inline-flex;
  align-items: center;
  justify-content:center
}

input[type="checkbox"]:after{
  font-family: "Font Awesome 5 Free";
  content: "\f00c";
  font-weight: 900;
  font-size:20px;
  color: rgb(137,207,240);
  display:none
}
input[type="checkbox"]:hover{
  background-color: rgb(137,207,240);
}

input[type="checkbox"]:checked{
  background-color:  rgb(244, 194, 194);
  height: 20px;
  width:20px;
}

input[type="checkbox"]:checked::after{
  display: block;
}
.completed {
  text-decoration: line-through;
  color: black;
}
</style>