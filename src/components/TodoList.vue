<script setup>
import TodoItem from './TodoItem.vue'

defineProps(['todos'])
defineEmits(['update-todo', 'remove-todo'])
</script>

<template>
  <section class="todo-list">
    <h3>TAREAS</h3>
    <div class="list">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="todo.createAt"
        :todo="todo"
        @update:done="val => todos[index].done = val"
        @update:content="val => todos[index].content = val"
        @delete="$emit('remove-todo', index)"
      />
    </div>
  </section>
</template>
