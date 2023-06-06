<script setup lang="ts">
  import { ref } from 'vue'
  import ColorInput from './components/ColorInput.vue'
  import GeneratedColors from './components/GeneratedColors.vue'
  import { useDark, useToggle } from '@vueuse/core'

  const isDark = useDark()
  const toggleDark = useToggle(isDark)

  const generatedCombs = ref<string[][]>([])

  function generated(combs: string[][]) {
    generatedCombs.value = combs
  }
</script>

<template>
  <nav>
    <h2>ColorGenerator</h2>
    <button @click="toggleDark()">{{ isDark ? '🌒' : '☀️' }}</button>
  </nav>
  <ColorInput v-on:@generate="generated" />
  <GeneratedColors :combinations="generatedCombs" />
</template>

<style scoped>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
