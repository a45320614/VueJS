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

<style>
</style>