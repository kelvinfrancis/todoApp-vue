<script setup>
defineProps(['name'])
defineEmits(['update:name'])
</script>

<template>
  <section class="greeting">
    <h2 class="title">
      Hola!, <input type="text" placeholder="Ingresa tu nombre" :value="name" @input="$emit('update:name', $event.target.value)" />
    </h2>
  </section>
</template>
