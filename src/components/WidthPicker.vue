<script setup>
import { computed } from 'vue'

const props = defineProps({
  label: {
    type: String,
    default: 'Percentage'
  },
  defaultWidth: {
    type: Number,
    default: 30
  }
})
defineEmits(['widthChanged'])

const widthValue = computed(() => props.defaultWidth + '%')
</script>

<template>
  <div>{{ label }}</div>
  <div class="wrapper">
    {{ widthValue }}
    <input
      class="percentage-input"
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
  align-items: center;
  gap: 15px; /* Space between the value and the input */
  margin: 10px 0 20px;
  padding-right: 30px;
}

.width-value {
  font-size: 16px;
  font-weight: bold;
  color: #333; /* Darker text color */
}

input[type='range'] {
  -webkit-appearance: none;
  appearance: none;
  height: 8px;
  background: #797777; /* Track color */
  border-radius: 5px;
  outline: none;
  transition: background 0.3s ease-in-out;
}

input[type='range']::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  background: #007bff; /* Blue thumb color */
  border-radius: 50%;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

input[type='range']::-moz-range-thumb {
  width: 20px;
  height: 20px;
  background: #007bff;
  border-radius: 50%;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

input[type='range']:hover {
  background: #524f4f; /* Darker track on hover */
}

input[type='range']::-webkit-slider-thumb:hover {
  background: #0056b3; /* Darker thumb on hover */
}

input[type='range']::-moz-range-thumb:hover {
  background: #0056b3;
}

.percentage-input {
  flex-grow: 1; /* Makes the range input stretch */
}
</style>
