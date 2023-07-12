<script setup lang="ts">
  import { computed, ref, watch } from 'vue';
  import ColorCard from './ColorCard.vue';
  import SavedColors from './SavedColors.vue';
  import type Combination from '../types/Combination';

  const props = defineProps<{
    combinations: Combination[];
    reset: Boolean;
  }>();

  computed(() => {
    if (props.reset === true) {
      console.log('reset');
    }
  });

  watch(
    () => props.reset,
    () => {
      savedColorsArray.value = [];
    },
  );

  const savedColorsArray = ref<Combination[]>([]);

  function savedColorToArray(colorCard: Combination) {
    if (colorCard.checked === true) {
      savedColorsArray.value.push(colorCard);
    } else {
      const index = savedColorsArray.value.findIndex((savedItem) => savedItem.id === colorCard.id);
      if (index > -1) {
        savedColorsArray.value.splice(index, 1);
      }
    }
  }
</script>
<template>
  <div>Total Combinations: {{ combinations.length }}</div>
  <div class="generatedColors">
    <ColorCard
      v-for="comb in props.combinations"
      :color-card="comb"
      :color-code="comb.combination"
      @@save-color="savedColorToArray(comb)"
      :key="comb.id"
    />
  </div>
  <div class="savedColors">
    <SavedColors :saved-colors="savedColorsArray" :reset="props.reset" />
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
