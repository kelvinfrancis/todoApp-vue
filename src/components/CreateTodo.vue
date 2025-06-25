<script setup>
defineProps(['inputContent', 'inputCategory'])
defineEmits(['update:inputContent', 'update:inputCategory', 'add-todo'])

</script>

<template>
  <section class="create-todo">
    <h3>AGREGA UNA TAREA</h3>
    <form @submit.prevent="$emit('add-todo')">
      <h4>¿Qué necesitas agregar a tus tareas?</h4>
      <input 
        type="text" 
        placeholder="ej. Terminar la actividad final" 
        :value="inputContent" 
        @input="$emit('update:inputContent', $event.target.value)"
      />
      <h4>Elige una categoría</h4>
      <div class="options">
        <label>
          <input type="radio" name="category" value="Estudios" :checked="inputCategory === 'Estudios'" @change="$emit('update:inputCategory', 'business')" />
          <span class="bubble business"></span><div>Estudios</div>
        </label>
        <label>
          <input type="radio" name="category" value="Personal" :checked="inputCategory === 'Personal'" @change="$emit('update:inputCategory', 'personal')" />
          <span class="bubble personal"></span><div>Personal</div>
        </label>
      </div>
      <input type="submit" value="Agregar tarea" />
    </form>
  </section>
</template>
