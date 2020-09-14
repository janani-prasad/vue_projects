<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodoItem"/>
    <Todos :todos="todos" v-on:del-todo="deleteItem">
      
    </Todos>
  </div>
</template>

<script>

import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue'
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteItem(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodoItem(newTodo) {
      console.log(newTodo)
      this.todos = [...this.todos, newTodo];
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5').then(response => this.todos = response.data).catch(e => console.log(e))
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
