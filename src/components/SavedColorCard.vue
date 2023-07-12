<script setup lang="ts">
  import { ref } from 'vue';
  import type Combination from '../types/Combination';
  const props = defineProps<{
    combination: Combination;
  }>();

  const colorCode = ref<string>(props.combination.combination);

  const nameInput = ref('');

  function addNameToSavedArray() {
    props.combination.name = nameInput.value;
  }
</script>

<template>
  <div class="colorCard">
    <div class="colorName">
      Name:
      <input @keyup="addNameToSavedArray" type="text" placeholder="color name e.g.primary" v-model="nameInput" />
    </div>
    <div class="colorWrapper">
      <p class="colorCode">#{{ colorCode }}</p>
      <div class="colorPreview">{{ combination.name }}</div>
    </div>
    <p class="removeFromSaved" @click="$emit('@removeFromSaved', combination.id), (combination.checked = false)" style="cursor: pointer">
      🅧
    </p>
  </div>
</template>

<style scoped>
  .colorCard {
    position: relative;
    display: flex;
    flex-direction: column;
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

  .removeFromSaved {
    position: absolute;
    top: 3.5rem;
    right: -0.5rem;
  }

  .colorWrapper {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 0.5rem;
  }

  .colorName {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 1rem;
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

  .colorName input {
    text-align: center;
  }
</style>
