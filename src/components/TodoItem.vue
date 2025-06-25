<script setup>
defineProps(['todo'])
defineEmits(['update:done', 'update:content', 'delete'])

</script>

<template>
  <div :class="`todo-item ${todo.done && 'done'}`">
    <label>
      <input type="checkbox" :checked="todo.done" @change="$emit('update:done', $event.target.checked)" />
      <span :class="`bubble ${todo.category}`"></span>
    </label>

    <div class="todo-content">
      <input type="text" :value="todo.content" @input="$emit('update:content', $event.target.value)" />
    </div>

    <div class="actions">
      <button class="delete" @click="$emit('delete')">Delete</button>
    </div>
  </div>
</template>
