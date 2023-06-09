<script setup lang="ts"></script>
<template>
  <div class="instructions">
    <div>
      <h4>What is it?</h4>
      <p>
        <span>hexie.</span> is a fun color generator that helps designers to find a combination of colors that will support the identity of
        a brand by generating a hexcode of the color according to the given input.
      </p>
      <p>
        Try a brand keyword or the initials of an athlete with a jersey number. e.g. fa14 (F1 driver Fernando Alonso 🏎️) or f1, d07, face,
        etc.
      </p>
      <p>Generated colors include only inputed characters in all possible combinations.</p>
    </div>
    <div>
      <h4>How to use?</h4>
      <p>
        Enter desired hexcode characters. By checking a color you put it to saved list where you can name the color e.g. primary, secondary,
        and copy to clipboard to share the picked color to a developer.
      </p>
      <p>Have fun 🎉</p>
      <p><strong>Note:</strong> I understand that this might be useless. But i learned a lot during building this small project ✌️</p>
    </div>
  </div>
</template>
<style scoped>
  .instructions {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  span {
    font-family: 'Lobster', cursive;
    font-size: 1.5rem;
  }
</style>
