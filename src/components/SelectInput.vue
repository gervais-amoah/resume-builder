<script setup>
defineProps({
  label: {
    type: String,
    default: 'Weight'
  },
  options: {
    type: Array,
    default: () => [
      { name: 'Option 1', value: 'value 1' },
      { name: 'Option 2', value: 'value 2' }
    ]
  },
  defaultOption: {
    type: String
  }
})

defineEmits(['updateSelection'])
</script>

<template>
  <div>
    <label for="">
      <select @change="$emit('updateSelection', $event.target.value)" :name="label">
        <option
          v-for="option in options"
          :value="option.value"
          :key="option.value"
          :selected="defaultOption === option.value"
        >
          {{ option.name }}
        </option>
      </select>
      {{ label }}
    </label>
  </div>
</template>

<style scoped>
select {
  display: inline-block;
  min-width: 80px;
  height: 25px;
  margin-right: 8px;
  margin-bottom: 10px;
}
</style>
