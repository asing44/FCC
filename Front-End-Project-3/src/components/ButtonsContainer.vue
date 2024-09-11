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

const props = defineProps(['bankCheck'])


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
  })

  Draggable.create(".volume__slider", {
    type: "x",
    bounds: document.getElementsByClassName("volume__slider-background")[0],
    inertia: true,
    onDragStart: function () {
      volumeLabel.style.display = "block";
      volumeCopy_animation.timeScale(1);
      volumeCopy_animation.play();
    },
    onDrag: function () {
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
})

function btnClick(e) {
  let btn = e.target;
  btn.nextElementSibling.volume = volumeCopy / 100;
  console.log(volumeCopy / 100);
  btn.nextElementSibling.play();
}

</script>

<template>
  <section v-if="bankCheck" class="buttons__container buttons__heater">
    <Button @click="btnClick" @keydown.q="btnClick">
      <template #button-slot>
        Q
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-1.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick" @keydown.w="btnClick">
      <template #button-slot>
        W
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-2.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        E
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-3.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        A
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Kick_n_Hat.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        S
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Cev_H2.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        D
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Dsc_Oh.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        Z
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/RP4_KICK_1.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        X
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-4_1.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        C
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-6.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
  </section>
  <section v-else class="buttons__container buttons__piano">
    <Button @click="btnClick">
      <template #button-slot>
        Q
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-2.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        W
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-1.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        E
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-3.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        A
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Kick_n_Hat.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        S
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Cev_H2.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        D
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Dsc_Oh.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        Z
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/RP4_KICK_1.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        X
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-4_1.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
    <Button @click="btnClick">
      <template #button-slot>
        C
      </template>
      <template #audio-slot>
        <audio class="button__audio">
          <source src="../assets/audio/Heater-6.mp3" type="audio/mpeg">
        </audio>
      </template>
    </Button>
  </section>
</template>