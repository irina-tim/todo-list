<template>
  <div id="app">
    <TodoList/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
  body {
    background-color: #42A1EC;
    margin: 0;
    height: 100vh;
  }
</style>
