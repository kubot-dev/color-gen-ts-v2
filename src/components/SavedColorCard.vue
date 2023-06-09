<script setup lang="ts">
  import { ref } from 'vue'
  import type Combination from '../types/Combination'
  const props = defineProps<{
    combination: Combination
  }>()

  const colorCode = ref<string>(props.combination.combination)

  const showColorName = ref(false)

  const nameInput = ref('')

  function addNameToSavedArray() {
    props.combination.name = nameInput.value
  }
</script>

<template>
  <div class="colorCard" @mouseenter="showColorName = true" @mouseleave="showColorName = false">
    <p class="colorCode">#{{ colorCode }}</p>
    <div class="colorPreview">
      <p>{{ combination.name }}</p>
      <div class="savedColorName" v-if="showColorName">
        <form @submit.prevent="addNameToSavedArray">
          <input type="text" placeholder="color name e.g.primary" v-model="nameInput" />
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .colorCard {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    gap: 0.5rem;

    /* max-width: 320px; */
    height: auto;
    border: 1px solid v-bind('#' + colorCode + 50);
    box-shadow: 0rem 0rem 1rem v-bind('#' + colorCode + 50);
    border-radius: 1rem;
    padding: 1rem;
  }

  .dark .colorCard {
    border: 1px solid v-bind('#' + colorCode + 50);
    box-shadow: 0rem 0rem 1rem v-bind('#' + colorCode + 50);
  }

  .colorCode {
    font-weight: bold;
  }
  .colorPreview {
    position: relative;
    width: 150px;
    height: 75px;
    background-color: v-bind('#' + colorCode);
    border-radius: 0.5rem;
    color: #1f1f1ff1;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .savedColorName {
    position: absolute;
    background-color: #f1f1f1f9;
    border-radius: inherit;
    inset: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .dark .savedColorName {
    background-color: #1f1f1ff1;
  }

  .savedColorName input {
    text-align: center;
  }
</style>
