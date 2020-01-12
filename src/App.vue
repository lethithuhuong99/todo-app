<template>
  <div>
    <create-todo v-on:create-todo="addTodo"></create-todo>
    <div id="app">
      <button
      class="ui yellow button"
      v-on:click="clearCompleted">
      <i class="check icon"></i> Clear completed
      </button>
      <button
      class="ui red button"
      v-on:click="clearAll">
      <i class='trash icon'></i> Clear all
      </button>
    </div>
    <todo-list v-bind:todos="todos"></todo-list>
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

  // data function avails data to the template
  data() {
    return {
      todos: [],
    };
  },

  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    clearAll() {
      this.todos = [];
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.done);
    },
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

header {
  text-align: center;
  margin-top:50px;
}

body {
  background-image: linear-gradient(to right, rgba(152, 226, 250,0), rgba(55, 201, 250,1));
}
footer {
  margin-bottom: 20px;
  text-align : right;
}
</style>
