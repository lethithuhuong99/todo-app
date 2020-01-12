<template>
  <div>
    <todo-list v-bind:todos="todos"></todo-list>
    <create-todo v-on:create-todo="addTodo"></create-todo>
  </div>

</template>

<script>

import TodoList from './components/TodoList';
import CreateTodo from './components/CreateTodo';

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo,
  },

  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
  },

  // data function avails data to the template
  data() {
    return {
      todos: [],
    };
  },
  mounted() {
    /* console.log('App mounted!'); */
    if (localStorage.getItem('todos')) {
      this.todos = JSON.parse(localStorage.getItem('todos'));
    }
  },

  watch: {
    todos: {
      handler() {
      /* console.log('Todos changed!'); */
        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      deep: true,
    },
  },
};

</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.title{
  text-align: center;
  margin-top:50px;
}
</style>
