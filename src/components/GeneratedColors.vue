<script setup lang="ts">
  import { ref } from 'vue'
  import ColorCard from './ColorCard.vue'
  import SavedColors from './SavedColors.vue'

  const props = defineProps<{
    combinations: string[][]
  }>()

  const savedColorsArray = ref<string[]>([])

  function savedColorToArray(checked: boolean, bgColor: string) {
    if (checked === true) {
      savedColorsArray.value.push(bgColor)
    } else {
      savedColorsArray.value.pop()
    }
  }
</script>
<template>
  <div class="generatedColors">
    <ColorCard v-for="comb in props.combinations" :color-code="comb" @@save-color="savedColorToArray" />
  </div>
  <div class="savedColors">
    <SavedColors :saved-colors="savedColorsArray" />
  </div>
</template>
<style scoped>
  .generatedColors {
    display: flex;
    flex-flow: row wrap;
    gap: 1rem;
    margin-bottom: 1rem;
  }
</style>
