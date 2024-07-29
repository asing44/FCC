<script setup lang="ts">
import Buttons from "./components/Buttons.vue";
</script>

<template>
  <h1>FreeCodeCamp Drum Player!</h1>
  <main>
    <Buttons></Buttons>
  </main>
</template>

<style scoped>

h1 {
  margin-top: 3.2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
