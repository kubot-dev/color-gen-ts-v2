<script setup lang="ts">
  import { Teleport, computed } from 'vue'
  import { useClipboard } from '@vueuse/core'
  import SavedColorCard from './SavedColorCard.vue'
  import type Combination from '../types/Combination'

  const props = defineProps<{
    savedColors: Combination[]
  }>()

  const savedColorsOpened = computed(() => {
    if (props.savedColors.length > 0) {
      return true
    } else {
      return false
    }
  })

  const { copy } = useClipboard()

  const closeSavedColors = () => {
    props.savedColors.forEach((saved) => {
      saved.checked = false
    })
    props.savedColors.splice(0, props.savedColors.length)
  }

  function filterKeys(array: Combination[], key1: keyof Combination = 'name', key2: keyof Combination = 'combination') {
    return array.map((obj) => {
      const { [key1]: filteredKey1, [key2]: filteredKey2 } = obj
      return { [key1]: filteredKey1, [key2]: filteredKey2 }
    })
  }

  const saveToClipboard = () => {
    const filteredSavedObj = filterKeys(props.savedColors, 'name', 'combination')
    copy(JSON.stringify(filteredSavedObj))
  }
</script>
<template>
  <Teleport to="body">
    <div class="savedWrapper" :class="{ open: savedColorsOpened }">
      <h4>Saved Colors</h4>
      <SavedColorCard v-for="saved in props.savedColors" :combination="saved" :key="saved.id" />
      <button @click="closeSavedColors">Close</button>
      <button @click="saveToClipboard">Copy to clipboard (Json)</button>
    </div>
  </Teleport>
</template>
<style scoped>
  .savedWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 16px;
    position: fixed;
    height: 100vh;
    width: 360px;
    right: 0;
    background-color: #f1f1f1f9;
    box-shadow: 0rem 0rem 2rem #1f1f1ff1;
    padding: 1rem;
    transform: translateX(720px);
    transition: transform 250ms ease-in-out;
  }

  .dark .savedWrapper {
    background-color: #1f1f1ff1;
    box-shadow: 0rem 0rem 2rem #1f1f1ff1;
  }

  .savedWrapper.open {
    transform: translateX(0px);
  }
</style>
