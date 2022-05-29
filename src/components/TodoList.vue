<template>
  <div class="page">
    <header class="header">
      <h1 class="header__title">TODO list</h1>
      <form class="header__form">
        <input class="header__input" placeholder="What needs to be done?" @keyup.enter="addTask" v-bind:value="inputValue" v-on:input="handleInput">
        <button class="header__button" type="submit" v-on:click="addTask">Add new task</button>
      </form>
    </header>
    <List
      title="To Do"
      listName="todos"
      :list="todos"
      :editedTodo="editedTodo"
      @removeTodo="removeTodo"
      @mark="mark"
      @editTodo="editTodo"
      @doneEdit="doneEdit"
      @cancelEdit="cancelEdit"
    />
    <List
      title="Done"
      listName="completed"
      :list="completed"
      :editedTodo="editedTodo"
      @removeTodo="removeTodo"
      @mark="mark"
      @editTodo="editTodo"
      @doneEdit="doneEdit"
      @cancelEdit="cancelEdit"
    />
    <footer class="footer">
    </footer>
  </div>
</template>

<script type = "text/javascript">
/* eslint-disable */
  import List from './List.vue'
  export default {
    // App initial state
    data: () => ({
      todos: [],
      completed: [],
      inputValue: "",
      editedTodo: null
    }),

    methods: {
      handleInput(e) {
        this.inputValue = e.target.value.trim();
      },

      addTask(e) {
        e.preventDefault();
        if (!this.inputValue) {
            return;
        };
        this.todos.push({
            id: Date.now(),
            title: this.inputValue
        });
        this.inputValue = "";
      },

      removeTodo(todo, listType) {
        listType === "todos" ?
          this.todos.splice(this.todos.indexOf(todo), 1) :
          this.completed.splice(this.completed.indexOf(todo), 1);
      },

      mark(i, done) {
        done ?
          this.completed.push(...this.todos.splice(i, 1)) :
          this.todos.push(...this.completed.splice(i, 1));
      },

      editTodo(todo) {
        this.todoBeforeEdit = todo.title;
        this.editedTodo = todo;
      },

      doneEdit(todo, listType) {
        if (!this.editedTodo) { return }
        this.editedTodo = null;
        todo.title = todo.title.trim();
        if (!todo.title) {
             this.removeTodo(todo, listType);
          }
      },

      cancelEdit(todo) {
        this.editedTodo = null;
        todo.title = this.todoBeforeEdit;
      }
    },
    components: { List }
}
</script>

<style>
</style>
