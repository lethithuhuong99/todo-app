<template>
  <div id="app">
    <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <todo
    v-on:delete-todo="deleteTodo"
    v-on:complete-todo="completeTodo"
    v-for="todo in todos"
    :key="todo.id"
    v-bind:todo="todo"></todo>
  </div>
</template>

<script type = "text/javascript" >

import Swal from 'sweetalert2';
import Todo from './Todo';

export default {
  props: ['todos'],
  components: {
    Todo,
  },
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = !this.todos[todoIndex].done;
      if (this.todos[todoIndex].done) {
        Swal.fire(
          'Success!',
          'To-Do completed!',
          'success',
        );
      } else {
        Swal.fire(
          'Pending!',
          'To-Do pending!',
          'info',
        );
      }
    },

  },
};
</script>
