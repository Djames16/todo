<script setup>
import {ref} from 'vue'
let todos = ref (['A','B','C'])
let newTodo = ref('')
</script>

<template>

  <h1>My Todo Application</h1>
<ol>
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ol>

<input v-model="newTodo">
<button> Add Todo</button>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
body  {
    background: rgb(88,50,108);
background: linear-gradient(117deg, rgb(244, 194, 194) 0%, rgb(137,207,240) 100%);
font-family: 'Bruno Ace SC', cursive;
    text-align: center;
    min-height: 100vh;
}
</style>
