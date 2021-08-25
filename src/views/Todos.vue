<template>
  <h2>Todo</h2>
      <router-link to="/">Home</router-link>
      <hr>
  <AddTodo
    @add-todo="addTodo"
  />

  <select v-model="filterMethod">
    <option value="all">All</option>
    <option value="completed">Completed</option>
    <option value="uncompleted">Uncompleted</option>
  </select>

  <hr>

  <Loader v-if="loading" />

  <TodoList
    v-else-if="filteredTodos.length"
    v-bind:todos="filteredTodos"
    @remove-todo="removeTodo"
    @set-completed="setCompleted"
  />
  <p v-else>No todos!</p>
</template>

<script>
import TodoList from '@/components/TodoList/TodoList.vue';
import AddTodo from '@/components/AddTodo/AddTodo.vue';
import Loader from '@/components/Loader/Loader.vue';

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: false,
      filterMethod: 'all',
    };
  },
  components: {
    TodoList, 
    AddTodo,
    Loader,
  },
  mounted() {
    this.loading = true;
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(data => this.todos = data)
      .then(() => this.loading = false);
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
  },
  computed: {
    filteredTodos() {
      switch(true) {
        case this.filterMethod === 'completed':
          return this.todos.filter(todo => todo.completed);
        case this.filterMethod === 'uncompleted':
          return this.todos.filter(todo => !todo.completed);
        case this.filterMethod === 'all':
        default:
          return this.todos;
      }
    }
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
