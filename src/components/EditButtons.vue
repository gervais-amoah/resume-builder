<script setup>
const emit = defineEmits(['addClick', 'removeClick'])
</script>

<template>
  <div class="button-wrapper">
    <button class="edit-btn edit-btn-add" @click="emit('addClick')">+</button>
    <button class="edit-btn edit-btn-remove" @click="emit('removeClick')">-</button>
  </div>
</template>

<style scoped></style>
