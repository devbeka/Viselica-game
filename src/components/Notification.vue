<template>
  <div class="notification-container" :class="{ show: isVisable }">
    <p>Вы уже вводили этот символ!</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const isVisable = ref(false)

const openPopup = () => {
  isVisable.value = true
}
const closePopup = () => {
  isVisable.value = false
}

defineExpose({
  openPopup,
  closePopup
})
</script>

<style scoped>
@media (max-width: 550px) {
  div {
    display: none;
  }
}
</style>
