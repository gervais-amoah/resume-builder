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

<style scoped></style>
