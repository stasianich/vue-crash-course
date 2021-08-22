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

// 11:48 (time)
// https://www.youtube.com/watch?v=OlnwgS-gk8Y&ab_channel=%D0%92%D0%BB%D0%B0%D0%B4%D0%B8%D0%BB%D0%B5%D0%BD%D0%9C%D0%B8%D0%BD%D0%B8%D0%BD

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
