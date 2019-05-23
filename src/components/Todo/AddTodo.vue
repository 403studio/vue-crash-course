<template>
  <form @submit.prevent="submit">
    <input type="text" placeholder="Add todo" v-model="title">
    <input type="submit" value="Add">
  </form>
</template>

<script>
import uuid from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    submit() {
      const todo = {
        id: uuid.v4(),
        title: this.title,
        completed: false
      };
      this.title = "";
      this.$emit("add-todo", todo);
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 11;
  border: 1px solid #ccc;
  padding: 4px;
}
input[type="submit"] {
  flex: 1;
  border: 1px solid #ccc;
}
</style>
