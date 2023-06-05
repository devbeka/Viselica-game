<template>
  <Header />
  <div class="game-container">
    <Figure :wrongLettersCount="wrongLeters.length" />
    <WrongLetters :wrongLeters="wrongLeters" />
    <Word :word="word" :correctLeters="correctLeters" />
  </div>
  <Modal ref="modal" :word="word" @restart="restart" />
  <Notification ref="notification" />
</template>

<script setup lang="ts">
import { computed, ref, watch } from 'vue'
import { useRandomWord } from './composables/useRandomWord'
import Figure from './components/Figure.vue'
import Header from './components/Header.vue'
import Notification from './components/Notification.vue'
import Modal from './components/Modal.vue'
import Word from './components/Word.vue'
import WrongLetters from './components/WrongLetters.vue'

const { word, getRandomWord } = useRandomWord()

const letters = ref<string[]>([])
const correctLeters = computed(() => letters.value.filter((x) => word.value.includes(x)))
const wrongLeters = computed(() => letters.value.filter((x) => !word.value.includes(x)))
const isLose = computed(() => wrongLeters.value.length === 6)
const isWin = computed(() => [...word.value].every((x) => correctLeters.value.includes(x)))

const notification = ref<InstanceType<typeof Notification> | null>(null)
const modal = ref<InstanceType<typeof Modal> | null>(null)

watch(wrongLeters, () => {
  if (isLose.value) {
    modal.value?.openModal('lose')
  }
})
watch(correctLeters, () => {
  if (isWin.value) {
    modal.value?.openModal('win')
  }
})

const restart = async () => {
  await getRandomWord()
  letters.value = []
  modal.value?.closeModal()
}

window.addEventListener('keydown', ({ key }) => {
  if (isLose.value || isWin.value) {
    return
  }
  if (letters.value.includes(key)) {
    notification.value?.openPopup()
    setTimeout(() => notification.value?.closePopup(), 3000)
    return
  }
  if (/[а-яА-ЯёЁ]/.test(key)) {
    letters.value.push(key.toLocaleLowerCase())
  }
})
</script>
