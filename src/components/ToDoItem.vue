<template>
  <li class="todo-item" :class="{ isDone: done }">
    <input
      class="checkbox"
      type="checkbox"
      v-show="false"
      :id="id"
      :checked="done"
      @change="$emit('update:done', !done)"
    />
    
    <label
          class="checkbox-label" 
          v-show="!editing"
          :for="id"
          @dblclick="editTitle"
          >
        <i v-show="done" class="far fa-check-square"></i>
        <i v-show="!done" class="far fa-square"></i>
        <span>{{ title }}</span>
    </label>
    <button class="to-do-del-btn" @click="$emit('removeTodo', id)">
      Delete
    </button>
    <input
      class="todo-edit"
      type="text"
      ref="input"
      v-if="editing"
      v-model="editedTitle"
      @keyup.enter="doneEdit()"
      @keyup.esc="cancelEdit()"
    />
    
  </li>
</template>

<script>
export default {
  props: {
    id: { type: Number, required: true },
    title: { type: String, required: true },
    done: { type: Boolean, default: false },
  },
  data() {
    return {
      editing: false,
      editedTitle: "",
    };
  },
  methods: {
    editTitle() {
      this.editing = true;
      this.editedTitle = this.title;
      this.$nextTick(() => {
        this.$refs.input.focus();
      });
    },
    doneEdit() {
      if (!this.editing) return;
      this.editedTitle = this.editedTitle.trim();
      this.editedTitle
        ? this.$emit("update:title", this.editedTitle)
        : this.$emit("removeTodo", this.id);
      this.editing = false;
    },
    cancelEdit() {
      this.editing = false;
    },
  },
  
};
</script>

<style scoped>
/* Scoped 會使 css 只作用在這個 Component */
.todo-item {
  box-sizing: border-box;
  display: flex;
  font-size: 1.25rem;
  padding: 5px;
  width: 100%;
  align-items: center;
  transition: 0.2s;
}
.checkbox-label {
  flex-grow: 1;
}
.far,
.fas {
  color: #8f8f8f;
  padding: 0 10px;
}
.far:hover,
.fas:hover {
  color: #cccccc;
}
.todo-edit {
  box-sizing: border-box;
  background: #222222;
  border: 0px solid black;
  border-radius: 10px;
  color: white;
  font-size: 1.25rem;
  flex-grow: 1;
  height: 100%;
  width: 100%;
  transition: 0.4s;
  outline: none;
}
.todo-item:first-child {
  margin-top: 10px;
}
.todo-item:last-child {
  margin-bottom: 10px;
}
.todo-item:hover {
  background: #121212;
  border-radius: 10px;
}
.todo-item.isDone label span {
  color: gray;
  text-decoration: line-through;
}
.todo-item.isDone label i {
  color: gray;
}
.todo-item .fa-times {
  /* visibillity 也可 opacity 可保證click event*/
  opacity: 0;
}
.todo-item:hover .fa-times {
  opacity: 1;
}
.to-do-del-btn {
  background: none;
  border-radius: 9999px;
  color: white;
}
</style>