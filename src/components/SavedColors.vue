<script setup lang="ts">
  import { Teleport, ref, watch } from 'vue';
  import { useClipboard } from '@vueuse/core';
  import SavedColorCard from './SavedColorCard.vue';
  import type Combination from '../types/Combination';

  const props = defineProps<{
    savedColors: Combination[];
    reset: Boolean;
  }>();

  // const savedColorsOpened = computed(() => {
  //   if (props.savedColors.length > 0) {
  //     return true;
  //   } else {
  //     return false;
  //   }
  // });

  const savedColorsShown = ref(false);

  watch(
    () => props.reset,
    () => {
      savedColorsShown.value = false;
    },
  );

  function toggleSavedOpened() {
    savedColorsShown.value = !savedColorsShown.value;
  }

  // const closeSavedColors = () => {
  //   props.savedColors.forEach((saved) => {
  //     saved.checked = false;
  //   });
  //   props.savedColors.splice(0, props.savedColors.length);
  // };

  const { copy } = useClipboard();

  function filterKeys(array: Combination[], key1: keyof Combination = 'name', key2: keyof Combination = 'combination') {
    return array.map((obj) => {
      const { [key1]: filteredKey1, [key2]: filteredKey2 } = obj;
      return { [key1]: filteredKey1, [key2]: filteredKey2 };
    });
  }

  const saveToClipboard = () => {
    const filteredSavedObj = filterKeys(props.savedColors, 'name', 'combination');
    copy(
      JSON.stringify(filteredSavedObj)
        .replace(/[[\]"]/g, '')
        .replace(/[,]/g, ', '),
    );
  };

  function removeFromSaved(e: Number) {
    const index = props.savedColors.findIndex((savedItem) => savedItem.id === e);

    if (index > -1) {
      props.savedColors.splice(index, 1);
    }
  }
</script>
<template>
  <Teleport to="body">
    <div class="savedWrapper" :class="{ open: savedColorsShown }">
      <div class="openArrow" @click="toggleSavedOpened">
        <div class="savedVertical">Saved Colors</div>
      </div>
      <h4>Saved Colors</h4>
      <SavedColorCard @@removeFromSaved="removeFromSaved" v-for="saved in props.savedColors" :combination="saved" :key="saved.id" />
      <button @click="saveToClipboard">Copy to clipboard</button>
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
    width: 320px;
    right: 0;
    background-color: #f1f1f1f9;
    filter: drop-shadow(0 0 1rem var(--color-dark-transparent));
    padding: 1rem;
    transform: translateX(320px);
    transition: transform 250ms ease-in-out;
  }

  .openArrow {
    position: absolute;
    background-color: inherit;
    padding: 1rem 0.5rem;
    border-radius: 0.5rem 0 0 0.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    left: -2.5rem;
    top: 50%;
    transform: translateY(-50%);
    border-right: none;
    cursor: pointer;
  }

  .savedVertical {
    background-color: inherit;
    writing-mode: vertical-rl;
    transform: rotate(180deg);
  }

  .openArrow:hover {
    border-top: 1px solid;
    border-left: 1px solid;
    border-bottom: 1px solid;
    border-color: var(--color-dark-transparent);
  }
  .dark .openArrow:hover {
    border-color: var(--color-light-transparent);
  }

  .dark .savedWrapper {
    background-color: #1f1f1ff1;
    filter: drop-shadow(0 0 1rem var(--color-light-transparent));
  }

  .savedWrapper.open {
    transform: translateX(0px);
  }
</style>
