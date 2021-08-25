<template>
  <div>
    <ul>
      <Todo
        v-for="(todo, i) of todos"
        v-bind:key="todo.id"
        v-bind:todo="todo"
        v-bind:index="i"
        v-on:remove-todo="removeTodo"
        v-on:set-completed="setCompleted"
      />
    </ul>
  </div>
</template>

<script>
import Todo from '@/components/Todo/Todo';

export default {
  props: [
    'todos',
  ],
  components: {
    Todo
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id)
    },
    setCompleted(id) {
      this.$emit('set-completed', id);
    }
  }
}
</script>

<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>
