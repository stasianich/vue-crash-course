<template>
  <div id="app">
    <h1>Todo</h1>
    <AddTodo
      @add-todo="addTodo"
    />
    <hr>
    <TodoList
      v-bind:todos="todos"
      @remove-todo="removeTodo"
      @set-completed="setCompleted"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList/TodoList.vue';
import AddTodo from '@/components/AddTodo/AddTodo.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: 1, title: 'Todo 1', completed: false},
        {id: 2, title: 'Todo 2', completed: false},
        {id: 3, title: 'Todo 3', completed: false},
        {id: 4, title: 'Todo 4', completed: true},
        {id: 5, title: 'Todo 5', completed: true},
      ]
    };
  },
  components: {
    TodoList,
    AddTodo,
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    },
    setCompleted(id) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          return {
            ...todo,
            completed: !todo.completed,
          };
        }

        return todo;
      })
    },
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
