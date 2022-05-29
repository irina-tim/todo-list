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
        <input
          class="list__element-checkbox"
          type="checkbox"
          v-on:change="$emit('mark', i, listName === 'todos')"
          :checked="listName !== 'todos'"
        />
        <label class="list__element-label" @dblclick="$emit('editTodo', todo)">
          {{ todo.title }}
          </label>
        <input
          v-if="todo === editedTodo"
          class="list__element-edit"
          type="text"
          v-model="todo.title"
          @vnode-mounted="({ el }) => el.focus()"
          @blur="$emit('doneEdit', todo, listName)"
          @keyup.enter="$emit('doneEdit', todo, listName)"
          @keyup.escape="$emit('cancelEdit', todo)"
        />
        <button
          class="list__element-remove-button"
          @click="$emit('removeTodo', todo, listName)"
        >
          X
        </button>
      </li>
    </ul>
  </div>
</template>

<script type="text/javascript">
export default {
  props: ['title', 'listName', 'list', 'editedTodo', 'removeTodo', 'mark', 'editTodo', 'doneEdit', 'cancelEdit']
}
</script>
