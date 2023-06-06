<script setup lang="ts">
  const props = defineProps<{
    colorCode?: string
  }>()

</script>

<template>
  <div class="colorCard">
    <p class="colorCode">#{{ props.colorCode }}</p>
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
    border: 1px solid v-bind('#' + colorCode);
    box-shadow: 0rem 0rem 1rem v-bind('#' + colorCode);
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
    width: 150px;
    height: 75px;
    background-color: v-bind('#' + colorCode);
    border-radius: 0.5rem;
  }
</style>
