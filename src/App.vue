<template>
  <div id="app">
    <h1>Todo App</h1>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo"/>
  </div>
</template>

<script>
import axios from "axios";
import AddTodo from "./components/Todo/AddTodo.vue";
import Todos from "./components/Todo/Todos.vue";

export default {
  name: "app",
  components: {
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.unshift(todo);
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  },
  async created() {
    const res = await axios.get(
      "http://jsonplaceholder.typicode.com/todos?_limit=5"
    );
    this.todos = res.data;
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
h2 {
  margin: 0;
  padding: 5px 10px;
}
</style>
