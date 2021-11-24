<template>
  <div id="app">
    <ul>
      <to-do-input @addTodo="addTodo"></to-do-input>
      <to-do-item
        v-for="ToDoItem in ToDoItems"
        v-bind="ToDoItem"
        :title.sync="ToDoItem.title"
        :done.sync="ToDoItem.done"
        :key="ToDoItem.id"
        @removeTodo="removeTodo"
      ></to-do-item>
    </ul>
  </div>
</template>

<script>
import ToDoItem from "./components/ToDoItem";
import ToDoInput from "./components/ToDoInput";

export default {
  name: "App",
  components: {
    ToDoItem,
    ToDoInput
  },
  data() {
    return {
      maxID: 4,
      ToDoItems: [
        { id: 0, title: "Download Node.js", done: true },
        { id: 1, title: "Install Vue CLI", done: true },
        { id: 2, title: "Learn Vue", done: false },
        { id: 3, title: "Create a to-do list", done: false },
      ],
    };
  },
  methods: {
    addTodo(title) {
      this.ToDoItems.push({
        id: this.maxID++,
        title: title,
        done: false,
      });
    },
    removeTodo(id) {
      this.ToDoItems = this.ToDoItems.filter((todo) => todo.id !== id);
    },
  },
};
  



</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
