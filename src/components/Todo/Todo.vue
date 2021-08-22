<template>
  <li>
    <span v-bind:class="{completed: todo.completed}">
      <input
        type="checkbox"
        :checked="todo.completed"
        v-on:change="$emit('set-completed', todo.id)"
      >
      <strong>{{ index + 1 }}</strong>
      {{ todo.title }}
    </span>
    <button
      class="remove"
      v-on:click="$emit('remove-todo', todo.id)"
    >
      &times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number,
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 2rem;
    margin-bottom: 1rem;
  }

  .remove {
    background-color: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
  }

  input {
    margin-right: 1rem;
  }

  .completed {
    text-decoration: line-through;
  }
</style>
