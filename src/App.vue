<script setup>
import {ref} from 'vue'
let todos = ref (['A','B','C'])
</script>

<template>

  <h1>My Todo Application</h1>
<ol>
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ol>
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
</style>
