<script setup>
import BaseButton from './BaseButton.vue'

const exportPDF = () => {
  console.log('export pdf')
}
</script>

<template>
  <BaseButton btnType="primary" @click="exportPDF">Export PDF</BaseButton>
</template>

<style scoped></style>
