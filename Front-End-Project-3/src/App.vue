<script setup lang="ts">
import Buttons from "./components/ButtonsContainer.vue";

import { ref } from 'vue'

const powerCheck = ref(false);
const bankCheck = ref(false);

function powerToggle() {
  powerCheck.value = !powerCheck.value;
}

function bankToggle() {
  if (powerCheck.value == true) {
    bankCheck.value = !bankCheck.value;
  }
}
</script>

<template>
  <h1>FreeCodeCamp Drum Player!</h1>
  <div class="main-wrapper">
    <main>
      <section class="main__left">
        <Buttons></Buttons>
      </section>
      <section class="controls">
        <div class="controls__power-container controls__container">
          <p class="controls__power-heading heading">Power</p>
          <div class="controls__input-wrapper" @click="powerToggle">
            <div v-if="powerCheck" class="toggle--on toggle"></div>
            <div v-else class="toggle--off toggle"></div>
          </div>
        </div>
        <div class="controls__volume-container volume controls__container">
          <div class="volume__label-wrapper"></div>
          <div class="volume__slider-wrapper"></div>
        </div>
        <div class="controls__bank-container controls__container">
          <p class="controls__bank-heading heading">Bank</p>
          <div class="controls__input-wrapper" @click="bankToggle()">
            <div v-if="bankCheck" class="toggle--on toggle"></div>
            <div v-else class="toggle--off toggle"></div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<style scoped>

.main-wrapper {
  height: 100%;
  place-content: center;
}

main {
  display: grid;
  grid-template-columns: 1fr auto;
  column-gap: 30px;
  padding: 0.5rem;
  border: 2px solid gray;
}

.controls {
  display: flex;
  flex-wrap: nowrap;
  flex-direction: column;
  align-items: start;
  padding: 2rem 5rem;
  gap: 16px;
}

.heading {
  font-weight: 800;
  font-size: 24px;
  line-height: 120%;
}

.controls__container {
}

.controls__input-wrapper {
  width: 60px;
  cursor: pointer;
}

.toggle {
  position: relative;
  height: 25px;
  width: 100%;
  background-color: #EFEFEF;
}

.toggle--on::after {
  content: '';
  position: absolute;
  height: 75%;
  top: 12.5%;
  right: 5%;
  aspect-ratio: 1 / 1;
  background-color: #62A87C;
}

.toggle--off::after {
  content: '';
  position: absolute;
  height: 75%;
  top: 12.5%;
  left: 5%;
  aspect-ratio: 1 / 1;
  background-color: #E63946;
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
