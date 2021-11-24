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
  color: white;
  background: #292929;
  display: grid;
  place-items: center center;
  height: 100vh;
  width: 100vw;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
body {
  margin: 0;
}
h1 {
  font-size: 5rem;
}
main {
  background: #1d1d1d;
  border-radius: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  min-width: 300px;
  max-width: 550px;
  width: 100%;
}
ul {
  margin: 0;
  padding: 0;
  width: 100%;
}

.break {
  flex-basis: 100%;
  height: 0;
}
.clearBtn {
  background: #313131;
  border: none;
  border-radius: 8px;
  color: white;
  font-size: 1.25rem;
  padding: 10px 15px;
  transition: 0.2s;
}
.clearBtn:hover {
  background: #353535;
}

</style>
