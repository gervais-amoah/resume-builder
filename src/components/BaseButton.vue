<script setup>
import { computed } from 'vue'

const props = defineProps({
  btnType: {
    type: String,
    default: ''
  }
})

const customClass = computed(() => {
  return props.btnType && `btn-${props.btnType}`
})
</script>

<template>
  <button class="btn" :class="customClass">
    <slot />
  </button>
</template>

<style scoped>
.btn {
  display: inline-block;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  font-size: 16px;
  background-color: var(--background-color-left);
  color: #fff;
  border: 1px solid var(--highlight-color-left);
  cursor: pointer;
}
.btn:hover {
  background-color: var(--highlight-color-left);
}

.btn-primary {
  background-color: var(--background-color-left);
}
.btn-primary:hover {
  background-color: var(--highlight-color-left);
}

.btn-secondary {
  background-color: var(--background-color-left);
  color: var(--highlight-color-left);
}
.btn-secondary:hover {
  background-color: var(--highlight-color-left);
  color: var(--background-color-left);
}
</style>
