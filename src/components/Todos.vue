<template>
  <div>
    <h1>HELLO DUSTIN!!!</h1>
    <div v-for="todo in todos" v-bind:key="todo.id" class="link-class">
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos", "stuff"]
};
</script>

<style scoped>
.link-class {
  font-size: 1.1em;
}
</style>
