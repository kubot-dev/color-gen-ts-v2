<script setup lang="ts">
  import type Combination from '../types/Combination';

  const props = defineProps<{
    colorCard: Combination;
    colorCode: string;
  }>();

  const emit = defineEmits<{
    (e: '@saveColor', colorCard: Combination): void;
  }>();

  const saveColor = () => {
    props.colorCard.checked = !props.colorCard.checked;
    emit('@saveColor', props.colorCard);
  };
</script>

<template>
  <div class="colorCard" @click="saveColor">
    <input class="colorSelect" type="checkbox" v-model="props.colorCard.checked" />
    <p class="colorCode">#{{ props.colorCard.combination }}</p>
    <div class="colorPreview"></div>
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

    flex: 1 1 120px;
  }

  .dark .colorCard {
    border: 1px solid v-bind('#' + colorCode + 50);
    box-shadow: 0rem 0rem 1rem v-bind('#' + colorCode + 50);
  }

  .colorCode {
    font-weight: bold;
  }
  .colorPreview {
    width: 150px;
    height: 75px;
    background-color: v-bind('#' + colorCode);
    border-radius: 0.5rem;
  }
</style>
