<template>
  
    <input
      type="text"
      class="todo-input"
      placeholder="What needs to be done?"
      v-model="newTodoTitle"
      @keyup.enter="addTodo"
    />
  
</template>

<script>
export default {
  name: "ToDoInput",
  data() {
    return {
      newTodoTitle: "",
    };
  },
  methods: {
    addTodo() {
      if (!this.newTodoTitle.trim()) return;
      this.$emit("addTodo", this.newTodoTitle);
      this.newTodoTitle = "";
    },
  },
}
</script>

<style scoped>
.todo-form {
  height: 3rem;
  width: 100%;
}
.todo-input {
  box-sizing: border-box;
  background: #222222;
  border: 0px solid black;
  border-radius: 10px;
  color: white;
  font-size: 1.5rem;
  height: 100%;
  width: 100%;
  padding: 10px;
  transition: 0.4s;
}
.todo-input:hover {
  box-shadow: 0 0 5pt 0.5pt black;
}
.todo-input:focus {
  outline: white solid 0px;
  box-shadow: 0 0 5pt 1pt black;
}
</style>