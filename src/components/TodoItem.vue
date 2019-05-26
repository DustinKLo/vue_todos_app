<template>
  <div class="todo-item" v-bind:class="{ 'is-complete' : todo.completed }">
    <p>
      <input type="checkbox" v-on:change="markComplete" v-bind:checked="todo.completed === true">
      Task: {{ todo.title }}
      <button
        v-if="todo.completed === true"
        v-on:click="$emit('del-todo', todo.id)"
        class="del"
      >x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete: function() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>


<style scoped>
.todo-item {
  background: #f4f4f4;
  padding-top: 2px;
  padding-bottom: 2px;
  padding-left: 20px;
  padding-right: 5px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  /* border-radius: 50%; */
  cursor: pointer;
  float: right;
  font-size: 1.2em;
}
input[type="checkbox"] {
  transform: scale(2.5);
}
</style>
