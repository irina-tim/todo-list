<template>
  <div class="list">
    <h2 class="list__header">
      <span class="list__header-title">{{ title }}</span>
      <span class="list__header-counter">{{ list.length }}</span>
    </h2>
    <ul class="list__container">
      <li
        class="list__element"
        v-for="(todo, i) in list"
        :key="todo.id"
        :class="{ list__element_editing: todo === editedTodo }"
      >
        <div class="list__element-group">
          <input
            class="list__element-checkbox"
            type="checkbox"
            v-on:change="$emit('mark', i, listName === 'todos')"
            :checked="listName !== 'todos'"
          />
          <label class="list__element-label" @dblclick="handleLabelDbclick(todo)">
            {{ todo.title }}
          </label>
          <input
            v-if="todo === editedTodo"
            class="list__element-edit"
            type="text"
            v-model="todo.title"
            @blur="$emit('doneEdit', todo, listName)"
            @keyup.enter="$emit('doneEdit', todo, listName)"
            @keyup.escape="$emit('cancelEdit', todo)"
            ref="edit"
          />
        </div>
        <button
          class="list__element-remove-button button"
          @click="$emit('removeTodo', todo, listName)"
        >
          X
        </button>
      </li>
    </ul>
  </div>
</template>

<script type="text/javascript">
/* eslint-disable */
export default {
  props: ['title', 'listName', 'list', 'editedTodo', 'removeTodo', 'mark', 'editTodo', 'doneEdit', 'cancelEdit'],

  methods: {
    handleLabelDbclick(todo) {
      this.$emit('editTodo', todo);
      this.$nextTick(() => {
        this.$refs.edit[0].focus();
      })   
    },
  }
}
</script>

<style>
  .list {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 50%;
  }

  .list__header {
    color: white;
    font-size: 30px;
    display: flex;
    justify-content: space-between;
    width: 100%;
    border-bottom: 1px solid white;
    padding-bottom: 10px;
  }

  .list__container {
    margin: 0;
    padding: 0;
    width: 100%;
  }

  .list__element {
    list-style: none;
    color: white;
    font-family: Arial, sans-serif;
    font-size: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    margin-bottom: 10px;
  }

  .list__element-checkbox {
    height: 25px;
    width: 25px;
  }

  .list__element-remove-button {
    padding: 3px 7px;
  }

  .list__element-group {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 100%;
  }

  .list__element-edit {
    font-size: 17px;
    padding: 5px;
    border: none;
    border-radius: 4px;
    box-shadow: rgba(131, 192, 253, 0.5) 0 0 0 3px;
    max-width: 85%;
    flex: 1;
  }

  .list__element_editing .list__element-label {
    display: none;
  }

  .list__element-label {
    word-break: break-word;
    max-width: 90%;
  }

</style>
