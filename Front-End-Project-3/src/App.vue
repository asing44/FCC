<script setup lang="ts">
import Buttons from "./components/Buttons.vue";
</script>

<template>
  <h1>FreeCodeCamp Drum Player!</h1>
  <div class="main-wrapper">
    <main>
      <div class="main__left">
        <Buttons></Buttons>
      </div>
      <div class="main__right controls">
        
      </div>
    </main>
  </div>
</template>

<style scoped>

.main-wrapper {
  display: grid;
  height: 100%;
  place-content: center;
}

main {
  display: flex;
  padding: 0.5rem;
  border: 2px solid gray;
}

.main__right {

}

.main__left {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}

h1 {
  margin-top: 3.2rem;
  font-size: 2.5rem;
  font-weight: 700;
  text-align: center;
}

@media (min-width: 1024px) {
}
</style>
