<template>
  <div>
    <input type="text" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
</script>

<style scoped>
div {
  margin-top: 90px;
  display: none;
}

@media (max-width: 550px) {
  div {
    display: block;
  }
}
</style>
