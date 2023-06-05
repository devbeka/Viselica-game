<template>
  <div v-if="wrongLeters.length" class="wrong-letters-container">
    <div class="wrong-letters">
      <p>Ошибки:</p>
      <span v-for="(letter, index) in wrongLeters" :key="letter">
        {{ index === wrongLeters.length - 1 ? letter : `${letter}, ` }}
      </span>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  wrongLeters: string[]
}

defineProps<Props>()
</script>
