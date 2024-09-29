<script setup>
defineProps({
  showAddBtn: {
    type: Boolean,
    default: true
  },
  showRemoveBtn: {
    type: Boolean,
    default: true
  }
})
const emit = defineEmits(['addClick', 'removeClick'])
</script>

<template>
  <div class="button-wrapper">
    <button v-if="showAddBtn" class="edit-btn edit-btn-add" @click="emit('addClick')">+</button>
    <button v-if="showRemoveBtn" class="edit-btn edit-btn-remove" @click="emit('removeClick')">
      -
    </button>
  </div>
</template>

<style scoped>
.edit-btn {
  min-width: 20px;
  height: 20px;
  border-radius: 4px;
  border: none;
  background-color: transparent;
  margin-left: 8px;
}

.edit-btn-add {
  background-color: #3feee6;
  color: #000;
}

.edit-btn-add:hover {
  background-color: rgb(68, 219, 212);
}

.edit-btn-remove {
  background-color: #f97068;
  color: #fff;
}

.edit-btn-remove:hover {
  background-color: #e0635c;
}
</style>
