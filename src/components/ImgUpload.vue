<script setup>
const emit = defineEmits(['imageChanged'])

const changeImage = (e) => {
  console.log(e.target.files[0])
  const selectedFile = e.target.files[0]
  if (!selectedFile) return
  const reader = new FileReader()

  reader.onload = (e) => {
    console.log(e.target.result)
    emit('imageChanged', e.target.result)
  }
  // reader.onerror = (e) => {
  //   console.log(e) // an error occurred
  // }

  reader.readAsDataURL(selectedFile)
}
</script>

<template>
  <label
    >Upload Image
    <input type="file" accept="image/*" @change="changeImage" />
  </label>
</template>

<style scoped>
input[type='file'] {
  display: none;
}

label {
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  border: 1px solid var(--highlight-color-left);
  padding: 0.5rem 1rem;
  border-radius: 5px;
  background-color: var(--background-color-left);
  color: var(--text-color-left);
}
</style>
