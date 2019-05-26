<template>
  <div>
    <form v-on:submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo...">
      <input type="submit" name="Submit" class="btn">
    </form>
  </div>
</template>

<script>
import uuid from "uuid";

export default {
  name: "AddTodo",
  data: function() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo: function(e) {
      e.preventDefault();
      if (this.title.trim().length > 0) {
        const newTodo = {
          // id: uuid.v4(),
          title: this.title,
          completed: false
        };
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
  font-size: 2em;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
  font-size: 2em;
}

.btn:hover {
  background: #666;
}
</style>
