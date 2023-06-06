<script setup lang="ts">
  import { computed, ref } from 'vue'

  const colorInput = ref('')
  const processedInput = ref<string[]>([])
  const inputMaxLength: number = 3
  const inputCount = computed<number>(() => colorInput.value.length)
  const generatedCombinations = ref<string[][]>([])

  const generateCombinations = () => {
    generatedCombinations.value = cartesianProduct(
      processedInput.value,
      processedInput.value,
      processedInput.value,
      processedInput.value,
      processedInput.value,
      processedInput.value,
    )
    emit('@generate', generatedCombinations.value)
  }

  const emit = defineEmits<{
    (e: '@generate', combinations: string[][]): void
  }>()

  function cartesianProduct<T>(...arrays: T[][]): T[][] {
    return arrays.reduce<T[][]>(
      (acc, val) => {
        return acc.flatMap<T[]>((el) => {
          return val.map<T[]>((v) => {
            return el.concat(v)
          })
        })
      },
      [[]],
    )
  }

  const processInput = (event: Event) => {
    processedInput.value = colorInput.value.split('')

    const inputElement = event.target as HTMLInputElement
    let { value } = inputElement

    if (value.length > inputMaxLength) {
      value = value.slice(0, inputMaxLength)
      inputElement.value = value
    }

    colorInput.value = value
  }
</script>
<template>
  <div class="inputWrapper">
    <h4>input up to 3 hexcode characters 0-1, a-f</h4>
    <form class="input" @submit.prevent="generateCombinations">
      <input type="text" v-model="colorInput" @input="processInput" placeholder="input hex characters" />
      <button class="generateBtn">Generate Colors</button>
    </form>
    {{ inputCount }} / {{ inputMaxLength }}
  </div>
</template>
<style scoped>
  .inputWrapper {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .input {
    display: flex;
    gap: 1rem;
    align-items: center;
    justify-content: center;
  }
  .generateBtn {
    color: #1f1f1f;
    border: 1px solid #1f1f1f14;
    box-shadow: 0rem 0rem 1rem #1f1f1f14;
  }
  .dark .generateBtn {
    color: #f1f1f1;
    border: 1px solid #f1f1f114;
    box-shadow: 0rem 0rem 1rem #f1f1f114;
  }
</style>
