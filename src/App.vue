<script setup lang="ts">
  import { ref } from 'vue'
  import ColorInput from './components/ColorInput.vue'
  import GeneratedColors from './components/GeneratedColors.vue'
  import HowToUse from './components/HowToUse.vue'
  import { useDark, useToggle } from '@vueuse/core'
  import type Combination from './types/Combination'

  const isDark = useDark()
  const toggleDark = useToggle(isDark)

  const inputValue = ref('')

  const combinationsArray = ref<Combination[]>([])

  function cartesianProduct<T>(arrays: T[][]): T[][] {
    const result: T[][] = []

    function generateCombinations(currentArray: T[], currentIndex: number) {
      if (currentIndex === arrays.length) {
        result.push(currentArray.slice())
        return
      }

      const currentSubArray = arrays[currentIndex]
      for (let i = 0; i < currentSubArray.length; i++) {
        currentArray[currentIndex] = currentSubArray[i]
        generateCombinations(currentArray, currentIndex + 1)
      }
    }

    generateCombinations(new Array(arrays.length), 0)
    return result
  }

  function generateCombinations(input: string): Combination[] {
    const characters = input.split('')
    const combinations: Combination[] = []
    let id = 0

    const cartesianResult = cartesianProduct([characters, characters, characters, characters, characters, characters])

    for (const combination of cartesianResult) {
      const combinationString = combination.join('')
      if (containsAllCharacters(combinationString, characters)) {
        combinationsArray.value.push({ id: ++id, checked: false, combination: combinationString })
      }
    }

    return combinations
  }

  function containsAllCharacters(combination: string, characters: string[]): boolean {
    for (const character of characters) {
      if (!combination.includes(character)) {
        return false
      }
    }
    return true
  }

  const combinations = (passedInput: string) => {
    combinationsArray.value = []

    inputValue.value = passedInput

    generateCombinations(inputValue.value)
  }
</script>

<template>
  <nav>
    <h2 class="logo">hexie.</h2>
    <button @click="toggleDark()">{{ isDark ? '🌒' : '☀️' }}</button>
  </nav>
  <ColorInput @@generate="combinations" />
  <GeneratedColors :combinations="combinationsArray" />
  <HowToUse />
  <footer class="credit">built by <a target="_blank" href="https://kubot.dev/">kubot.dev</a></footer>
</template>

<style scoped>
  .logo {
    font-family: 'Lobster', cursive;
    font-size: 2.5rem;
    letter-spacing: 1px;
    transform: skew(-15deg, -5deg);
    transition: transform 150ms ease-out;
  }
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .credit {
    font-size: 0.75em;
    color: inherit;
    padding-bottom: 1rem;
  }

  .credit a {
    font-family: 'Lobster', cursive;
    text-decoration: none;
    color: inherit;
    font-size: 1.5em;
  }
  .credit a:hover {
    text-decoration: underline;
    text-underline-offset: 3px;
  }
</style>
