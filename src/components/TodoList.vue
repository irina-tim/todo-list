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
      <h2 class="list__header">
        <span class="list__header-title">To Do</span>
        <span class="list__header-counter">{{ todos.length }}</span>
      </h2>
      <ul class="list__container">
        <li class="list__element" v-for="(todo, i) in todos" :key="todo.id">
          <input class="list__element-checkbox" type="checkbox" v-on:change="mark(i, true)">
          <label class="list__element-label" @dblclick="editTodo(todo)">{{ todo.title }}</label>
          <button class="list__element-remove-button" @click="removeTodo(todo, 'todos')">X</button>
        </li>
      </ul>
    </div>
    <div class="list">
      <h2 class="list__header">
        <span class="list__header-title">Done</span>
        <span class="list__header-counter">{{ completed.length }}</span>
      </h2>
      <ul class="list__container">
        <li class="list__element" v-for="(todo, i) in completed" :key="todo.id">
          <input class="list__element-checkbox" type="checkbox" v-on:change="mark(i, false)" checked>
          <label class="list__element-label" @dblclick="editTodo(todo)">{{ todo.title }}</label>
          <button class="list__element-remove-button" @click="removeTodo(todo, 'completed')">X</button>
        </li>
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
        title: this.inputValue
      })
      this.inputValue = '';
    },

    removeTodo(todo, listType) {
      listType === 'todos' ?
        this.todos.splice(this.todos.indexOf(todo), 1) :
        this.completed.splice(this.completed.indexOf(todo), 1)
    },

    mark (i, done) {
      done ? 
        this.completed.push(...this.todos.splice(i, 1)) : 
        this.todos.push(...this.completed.splice(i, 1));
    },

  }
}
</script>

<style>
</style>
