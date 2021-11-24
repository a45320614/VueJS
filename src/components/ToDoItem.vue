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

<style>

</style>