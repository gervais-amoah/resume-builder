<script setup>
import BaseButton from './BaseButton.vue'

const exportPDF = () => {
  html2pdf()
    ?.set({ margin: 0, filename: 'resume' })
    ?.from(document.getElementById('resume'))
    ?.save()
}
</script>

<template>
  <div class="exportBtnWrapper">
    <BaseButton btnType="primary" @click="exportPDF">Export resume as PDF</BaseButton>
  </div>
</template>

<style scoped>
.exportBtnWrapper {
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
</style>
