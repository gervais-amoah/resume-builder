<script setup>
const { contact } = defineProps({
  contact: { type: Object, required: true }
})
const emit = defineEmits(['edit'])

const updateContact = (event, key) => {
  emit('edit', event.target.innerText, key)
}
</script>

<template>
  <ul>
    <li contenteditable @blur="updateContact($event, 'phone')">{{ contact.phone }}</li>
    <li contenteditable @blur="updateContact($event, 'email')">{{ contact.email }}</li>
    <li contenteditable @blur="updateContact($event, 'address')">{{ contact.address }}</li>
  </ul>
</template>

<style scoped></style>
