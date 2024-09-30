<script setup>

/* -------------------------------------------------------------------------- */
/*                                    Setup                                   */
/* -------------------------------------------------------------------------- */

import { ref, onMounted } from 'vue'

import Button from './ButtonItem.vue';

import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { Draggable } from "gsap/Draggable";

gsap.registerPlugin(ScrollTrigger, Draggable);

defineProps(['bankCheck'])

gsap.registerPlugin(ScrollTrigger, Draggable);

let minSlider = 0;
let maxSlider = 1;
let volumeCopy = 50;

onMounted(() => {
  /* -------------------------------------------------------------------------- */
  /*                                  Controls                                  */
  /* -------------------------------------------------------------------------- */

  const volumeSetting = document.getElementById("volumeSetting");
  const volumeLabel = document.getElementById("volumeLabel");

  const volumeCopy_animation = gsap.to(volumeLabel, {
    paused: true,
    duration: 1,
    opacity: 1,
    ease: "power1.inOut",
    onReverseComplete: () => {
      volumeLabel.style.display = "none";
      volumeSetting.style.display = "block";
    }
  });

  Draggable.create(".volume__slider", {
    type: "x",
    bounds: document.getElementsByClassName("volume__slider-background")[0],
    inertia: true,
    onDragStart: function () {
      volumeLabel.style.display = "block";
      volumeCopy_animation.timeScale(1);
      volumeCopy_animation.play();
    },
    onDrag: function showName() {
      minSlider = this.minX;
      maxSlider = this.maxX;
      volumeCopy = Math.round(gsap.utils.normalize(minSlider, maxSlider, this.x) * 100);
      if (volumeSetting?.textContent.length > 0) {
        volumeSetting.style.display = "none";
      }
      volumeLabel.innerText = volumeCopy.toString();
    },
    onDragEnd: function () {
      volumeCopy_animation.timeScale(0.7);
      volumeCopy_animation.reverse()
    }
  });

  let btns = gsap.utils.toArray(".button");

  window.addEventListener("keydown", (e) => {

    btns.forEach(b => {
      if (e.key.toUpperCase() == b.innerText) {
        b.nextElementSibling.volume = volumeCopy / 100;
        b.nextElementSibling.play();
      }
    })
  })
})


function btnClick(e) {
  let btn = e.target;
  btn.nextElementSibling.volume = volumeCopy / 100;
  btn.nextElementSibling.play();

  let a_btnLabel = gsap.timeline();

  volumeLabel.innerText = btn.nextElementSibling.childNodes[0].dataset.label;
  volumeSetting.style.display = "none";

  a_btnLabel.restart();
  // Button label animation
  a_btnLabel.to(volumeLabel, {
    keyframes: [
      { display: "block", duration: 0 },
      { opacity: 1, duration: 0.25, ease: "expo.out" },
      { opacity: 0, duration: 0.5, delay: 0.25 },
      { display: "none" }
    ],
    onComplete: function () {
      volumeLabel.style.display = "none"
    }
  });

}

</script>

<template>
  <section v-if="bankCheck" class="buttons__container buttons__heater">
    <Button id="Q" @click="btnClick">
      <template #button-slot>
        Q
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-1.mp3" type="audio/mpeg" data-label="Heater-1">
        </audio>
      </template>
    </Button>
    <Button id="W" @click="btnClick" @keydown.w="btnClick">
      <template #button-slot>
        W
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-2.mp3" type="audio/mpeg" data-label="Heater-2">
        </audio>
      </template>
    </Button>
    <Button id="E" @click="btnClick">
      <template #button-slot>
        E
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-3.mp3" type="audio/mpeg" data-label="Heater-3">
        </audio>
      </template>
    </Button>
    <Button id="A" @click="btnClick">
      <template #button-slot>
        A
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <label name="Kick"></label>
          <source src="../assets/audio/Kick_n_Hat.mp3" type="audio/mpeg" data-label="Kick">
        </audio>
      </template>
    </Button>
    <Button id="S" @click="btnClick">
      <template #button-slot>
        S
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Cev_H2.mp3" type="audio/mpeg" data-label="Cev">
        </audio>
      </template>
    </Button>
    <Button id="D" @click="btnClick">
      <template #button-slot>
        D
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Dsc_Oh.mp3" type="audio/mpeg" data-label="Dsc">
        </audio>
      </template>
    </Button>
    <Button id="Z" @click="btnClick">
      <template #button-slot>
        Z
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/RP4_KICK_1.mp3" type="audio/mpeg" data-label="RP4 Kick">
        </audio>
      </template>
    </Button>
    <Button id="X" @click="btnClick">
      <template #button-slot>
        X
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-4_1.mp3" type="audio/mpeg" data-label="Heater-4">
        </audio>
      </template>
    </Button>
    <Button id="C" @click="btnClick">
      <template #button-slot>
        C
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-6.mp3" type="audio/mpeg" data-label="Heater-6">
        </audio>
      </template>
    </Button>
  </section>
  <section v-else class="buttons__container buttons__piano">
    <Button @click="btnClick" label="Heater">
      <template #button-slot>
        Q
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-2.mp3" type="audio/mpeg" data-label="Heater-2">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        W
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-1.mp3" type="audio/mpeg" data-label="Heater-1">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        E
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-3.mp3" type="audio/mpeg" data-label="Heater-3">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        A
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Kick_n_Hat.mp3" type="audio/mpeg" data-label="Kick">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        S
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Cev_H2.mp3" type="audio/mpeg" data-label="Cev">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        D
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Dsc_Oh.mp3" type="audio/mpeg" data-label="Dsc">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        Z
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/RP4_KICK_1.mp3" type="audio/mpeg" data-label="RP4">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        X
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-4_1.mp3" type="audio/mpeg" data-label="Heater-4">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        C
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-6.mp3" type="audio/mpeg" data-label="Heater-6">
        </audio>
      </template>
    </Button>
  </section>
</template>