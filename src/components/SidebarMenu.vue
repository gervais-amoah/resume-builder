<script lang="ts" setup></script>

<template>
  <div class="sidebar">
    <slot></slot>
  </div>
</template>

<style scoped>
.sidebar {
  width: 300px;
  height: 100%;
  padding: 20px;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgb(230, 230, 230);
}
</style>
