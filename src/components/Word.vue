<template>
  <div class="container">
    <div class="word">
      <span v-for="(letter, index) in word" :key="index" class="letter">
        {{ correctLeters.includes(letter) ? letter : '' }}
      </span>
    </div>
    <KeyboardOnMobile />
  </div>
</template>

<script setup lang="ts">
import KeyboardOnMobile from './KeyboardOnMobile.vue'
interface Props {
  word: string
  correctLeters: string[]
}

defineProps<Props>()
</script>

<style scoped>
.container {
  text-align: center;
}
</style>
