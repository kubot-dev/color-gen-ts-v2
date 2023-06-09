<script setup lang="ts">
  import { computed, ref } from 'vue'

  const input = ref('')
  const inputMaxLength: number = 4
  const inputCount = computed<number>(() => input.value.length)

  const limitInput = (event: Event) => {
    const inputElement = event.target as HTMLInputElement
    let { value } = inputElement

    if (value.length > inputMaxLength) {
      value = value.slice(0, inputMaxLength)
      inputElement.value = value
    }

    input.value = value
  }
</script>
<template>
  <div class="inputWrapper">
    <h4>input up to 4 hexcode characters 0-1, a-f</h4>
    <form class="input" @submit.prevent="$emit('@generate', input)">
      <input type="text" @input="limitInput" v-model="input" placeholder="input hex characters" autofocus />
      <button class="generateBtn">Generate Colors</button>
    </form>
    <div>{{ inputCount }} / {{ inputMaxLength }}</div>
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
