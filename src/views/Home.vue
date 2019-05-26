<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "../components/Todos.vue";
import AddTodo from "../components/AddTodo.vue";
// import Header from "../components/layout/Header.vue";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  created: function() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .catch(err => console.error(err))
      .then(res => res.json())
      .then(res => {
        this.todos = res;
      });
  },
  data: function() {
    return {
      todos: [] // { id: 1, title: "title 111111", completed: true },
    };
  },
  methods: {
    deleteTodo: function(id) {
      fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
        method: "DELETE"
      })
        .catch(err => console.error(err))
        .then(res => res.json())
        .then(res => {
          // this.todos.filter(todo => todo.id !== id);  // alternate way
          const deleteIndex = this.todos.findIndex(i => i.id === id);
          this.todos.splice(deleteIndex, 1);
        });
    },
    addTodo: function(newTodo) {
      const { title, completed } = newTodo;
      const jsonBody = {
        title,
        completed
      };
      fetch("https://jsonplaceholder.typicode.com/todos", {
        method: "POST",
        body: JSON.stringify(jsonBody)
      })
        .catch(err => console.error(err))
        .then(res => res.json())
        .then(res => {
          // this.todos = [...this.todos, newTodo];  // alternate way
          this.todos.push(newTodo);
          // this.todos.push(res.data);
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: censter; */
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
