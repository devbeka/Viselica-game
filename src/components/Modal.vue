<template>
  <div v-show="isVisable" class="modal-container">
    <div class="modal">
      <h2 v-if="gameStatus === 'win'">Поздравляю, вы победили! 🥇</h2>
      <div v-else>
        <h2>Вы проиграли! ☹️</h2>
        <h3>имя: {{ word }}</h3>
      </div>
      <button @click="emit('restart')">Сыграть еще раз</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { gameStatus } from '../types/gameStatus'

interface Props {
  word: string
}
defineProps<Props>()

const gameStatus = ref<gameStatus | null>(null)
const isVisable = ref(false)

const openModal = (status: gameStatus) => {
  gameStatus.value = status
  isVisable.value = true
}
const closeModal = () => {
  isVisable.value = false
}

const emit = defineEmits<{
  (e: 'restart'): void
}>()

defineExpose({
  openModal,
  closeModal
})
</script>

<style scoped>
h2,
h3 {
  color: white;
}

h3 {
  margin-top: 15px;
}
</style>
