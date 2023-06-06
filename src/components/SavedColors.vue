<script setup lang="ts">
  import { Teleport, computed } from 'vue'
  import SavedColorCard from './SavedColorCard.vue'

  const props = defineProps<{
    savedColors: string[]
  }>()

  const savedColorsOpened = computed(() => {
    if (props.savedColors.length > 0) {
      return true
    } else {
      return false
    }
  })
</script>
<template>
  <Teleport to="body">
    <div class="savedWrapper" :class="{ open: savedColorsOpened }">
      <h4>Saved Colors</h4>
      <SavedColorCard v-for="saved in props.savedColors" :color-code="saved" />
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
    position: absolute;
    height: 100vh;
    width: 360px;
    right: 0;
    background-color: #1f1f1ff1;
    box-shadow: 0rem 0rem 2rem #f1f1f114;
    padding: 1rem;
    transform: translateX(720px);
    transition: transform 250ms ease-in-out;
  }

  .savedWrapper.open {
    transform: translateX(0px);
  }
</style>
