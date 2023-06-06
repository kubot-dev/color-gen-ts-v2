<script setup lang="ts">
  import { ref } from 'vue'

  const props = defineProps<{
    colorCode?: string[]
  }>()

  const bgColor = ref(props.colorCode?.join(''))

  const checked = ref(false)

  const emit = defineEmits<{
    (e: '@saveColor', checked: boolean, bgColor?: string): void
  }>()

  const saveColor = () => {
    checked.value = !checked.value
    emit('@saveColor', checked.value, bgColor.value)
  }
</script>

<template>
  <div class="colorCard" @click="saveColor">
    <input class="colorSelect" type="checkbox" v-model="checked" />
    <p class="colorCode">#{{ bgColor }}</p>
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
    border: 1px solid v-bind('#' + bgColor);
    box-shadow: 0rem 0rem 1rem v-bind('#' + bgColor);
    border-radius: 1rem;
    padding: 1rem;

    flex: 1 1 220px;
  }

  .dark .colorCard {
    border: 1px solid v-bind('#' + bgColor + 50);
    box-shadow: 0rem 0rem 1rem v-bind('#' + bgColor + 50);
  }

  .colorCode {
    font-weight: bold;
  }
  .colorPreview {
    width: 150px;
    height: 75px;
    background-color: v-bind('#' + bgColor);
    border-radius: 0.5rem;
  }
</style>
