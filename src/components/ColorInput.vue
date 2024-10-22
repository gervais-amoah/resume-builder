<script setup>
defineProps({
  label: {
    type: String,
    default: 'Choose a color'
  },
  defaultColor: {
    type: String
  }
})

defineEmits(['colorChanged'])
</script>

<template>
  <div class="wrapper">
    <input
      type="color"
      :value="defaultColor"
      class="color-picker"
      @input="$emit('colorChanged', $event.target.value)"
    />
    <label>
      {{ label }}
    </label>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
}
.color-picker {
  margin-right: 10px;
  width: 26px; /* offset strange height, width difference */
  height: 30px;
  padding: 0;
  border: none;
  background: transparent;
}
</style>
