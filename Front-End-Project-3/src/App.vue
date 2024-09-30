<script setup>
import buttonsContainer from "./components/ButtonsContainer.vue";

import { ref, onMounted } from 'vue'
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { Draggable } from "gsap/Draggable";

gsap.registerPlugin(ScrollTrigger, Draggable);

const powerCheck = ref(false);
const volumeCopy = ref("");
const bankCheck = ref(false);

function powerToggle() {
  powerCheck.value = !powerCheck.value;
}

function bankToggle() {
  if (powerCheck.value == true) {
    bankCheck.value = !bankCheck.value;
  }
  if (bankCheck.value) {
    volumeCopy.value = "Heater Kit"
  }
  else {
    volumeCopy.value = "Smooth Piano Kit"
  }
}
</script>

<template>
  <h1>FreeCodeCamp Drum Player!</h1>
  <div class="main-wrapper">
    <main id="drum-machine">
      <section id="display" class="buttons">
        <buttonsContainer :bankCheck></buttonsContainer>
      </section>
      <section class="controls">
        <div class="controls__power-container controls__container">
          <p class="controls__power-heading heading">Power</p>
          <div class="controls__input-wrapper" @click="powerToggle">
            <div v-if="powerCheck" class="toggle--on toggle --bs"></div>
            <div v-else class="toggle--off toggle --bs"></div>
          </div>
        </div>
        <div class="controls__volume-container volume controls__container">
          <div class="volume__label-wrapper --bs"><span id="volumeSetting">{{ volumeCopy }}</span><span
              id="volumeLabel"></span></div>
          <div class="volume__slider-container">
            <div class="volume__slider-background"></div>
            <div class="volume__slider"></div>
          </div>
        </div>
        <div class="controls__bank-container controls__container">
          <p class="controls__bank-heading heading">Bank</p>
          <div class="controls__input-wrapper" @click="bankToggle()">
            <div v-if="bankCheck" class="toggle--on toggle --bs"></div>
            <div v-else class="toggle--off toggle --bs"></div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<style scoped>

.main-wrapper {
  margin-top: 2rem;
  place-content: center;
  border-radius: 1rem;
  box-shadow: 2px 2px 4px 1px gray;
}

main {
  display: grid;
  grid-template-columns: 1fr auto;
  column-gap: 30px;
  padding: 2rem;
}

/* --------------------------------- Buttons -------------------------------- */

.buttons {

}

.buttons__container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

/* -------------------------------- Controls -------------------------------- */

.controls {
  display: flex;
  flex-wrap: nowrap;
  flex-direction: column;
  align-items: center;
  padding: 2rem 5rem;
  gap: 2.5rem;
}

.heading {
  font-weight: 800;
  font-size: 24px;
  line-height: 120%;
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
  border-radius: 1rem;
  background-color: #62A87C;
}

.toggle--off::after {
  content: '';
  position: absolute;
  height: 75%;
  top: 12.5%;
  left: 5%;
  aspect-ratio: 1 / 1;
  border-radius: 1rem;
  background-color: #E63946;
}

.volume {
  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
  color: black;
}

.volume__label-wrapper {
  display: flex;
  height: 4rem;
  width: 14rem;
  justify-content: center;
  align-items: center;
  padding: 0.25rem 1rem;
  border-radius: 1rem;
  background-color: #EFEFEF;
}

.volume__label-wrapper span {
  font-weight: bold;
  text-align: center;
}

.volume__slider-container {
  position: relative;
  padding: 0 1%;
}

.volume__slider-background {
  border: 1px solid gray;
  border-radius: 1rem;
}

.volume__slider {
  position: absolute;
  height: 1rem;
  width: 1rem;
  top: -0.5rem;
  left: 0;
  border: 1px solid gray;
  border-radius: 50%;
  background-color: gainsboro;
}

#volumeLabel {
  opacity: 0;
}

h1 {
  margin-top: 3.2rem;
  font-size: 2.5rem;
  font-weight: 700;
  text-align: center;
}

.--bs {
  border-radius: 1rem;
  box-shadow: 2px 2px 2px 1px gray;
}

@media (min-width: 1024px) {
}
</style>
