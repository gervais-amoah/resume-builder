<script setup>
import { computed } from 'vue'

const props = defineProps({
  defaultWidth: {
    type: Number,
    default: 30
  }
})
defineEmits(['widthChanged'])

const widthValue = computed(() => props.defaultWidth + '%')
</script>

<template>
  <div class="wrapper">
    {{ widthValue }}
    <input
      type="range"
      min="20"
      max="50"
      step="5"
      :value="defaultWidth"
      @input="$emit('widthChanged', +$event.target.value)"
    />
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  gap: 5px;
}
</style>
