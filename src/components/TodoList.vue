<template>
  <div class="page">
    <header class="header">
      <h1 class="header__title">TODO list</h1>
      <form class="header__form">
        <input class="header__input" placeholder="What needs to be done?" @keyup.enter="addTask" v-bind:value="inputValue" v-on:input="handleInput">
        <button class="header__button" type="submit" v-on:click="addTask">Add new task</button>
      </form>
    </header>
    <div class="list">
      <h2 class="list__header">To Do</h2>
      <ul class="list__container">
        <li class="list__element" v-for="todo in todos" :key="todo.id">
          <label class="list__element-label" @dblclick="editTodo(todo)">{{ todo.title }}</label>
            <button class="list__element-remove-button" @click="removeTodo(todo)">X</button>
        </li>
      </ul>
    </div>
    <div class="list">
      <h2 class="list__header">Done</h2>
      <ul class="list__container">
          <li class="list__element"> Todo 1 </li>
          <li class="list__element"> Todo 2 </li>
          <li class="list__element"> Todo 3 </li>
      </ul>
    </div>
    <footer class="footer">
    </footer>
  </div>
</template>

<script type = "text/javascript" >
export default {

  // App initial state
  data: () => ({
    todos: [],
    completed: [],
    inputValue: ''
  }),

/* eslint-disable */
  methods: {
    handleInput (e) {
      this.inputValue = e.target.value.trim();
    },

    addTask(e) {
      e.preventDefault();      
      if (!this.inputValue) { return };
      this.todos.push({
        id: Date.now(),
        title: this.inputValue,
      })
      this.inputValue = '';
    },

    removeTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1)
    }
  }
}
</script>

<style>
</style>
