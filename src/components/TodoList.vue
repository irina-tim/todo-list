<template>
  <div class="page">
    <header class="header">
      <h1 class="header__title">TODO list</h1>
      <form class="header__form">
        <input
          class="header__input"
          placeholder="What needs to be done?"
          @keyup.enter="addTask"
          v-bind:value="inputValue"
          v-on:input="handleInput">
        <button
          class="header__button button"
          type="submit"
          v-on:click="addTask">
          Add new task
        </button>
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
  .page {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-bottom: 30px;
  }

  .header {
    text-align: center;
    width: 60%;
    background-color: white;
    margin: 20px 0;
    padding-bottom: 20px;
  }

  .header__title {
    margin: 20px 0 20px;
    color: #0067B9;
    font-family: Arial, sans-serif;
    font-weight: 800;
  }

  .header__button {
    padding: 10px 20px;
  }

  .button {
    background-image: linear-gradient(#42A1EC, #0070C9);
    border: 1px solid #0077CC;
    border-radius: 4px;
    box-sizing: border-box;
    color: white;
    cursor: pointer;
    font-family: Arial,sans-serif;
    font-size: 17px;    
    text-align: center;
  }

  .button:disabled {
    cursor: default;
    opacity: .3;
  }

  .button:hover {
    background-image: linear-gradient(#51A9EE, #147BCD);
    border-color: #1482D0;
    text-decoration: none;
  }

  .button:active {
    background-image: linear-gradient(#3D94D9, #0067B9);
    border-color: #006DBC;
    outline: none;
  }

  .header__input {
    font-size: 17px;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    box-shadow: rgba(131, 192, 253, 0.5) 0 0 0 3px;
    margin-right: 10px;
    min-width: 200px;
    width: 40%;
  }

</style>
