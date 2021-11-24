<template>
  <li class="todo-item" :class="{}">
      
    <input
      class="checkbox"
      type="checkbox"
      :id="id"
      :checked="done"
      @change="$emit('update:done', !done)"
    />
    <label class="checkbox-label" :for="id">
        
      <span>{{ title }}</span>
    </label>
    
    
    
  </li>
  
</template>

<script>
export default {
  props: {
    id: { type: Number, required: true },
    title: { type: String, required: true },
    done: { type: Boolean, default: false },
  },
  
};
</script>

<style>

</style>