<script setup>
import ClockEyebrow from './components/ClockEyebrows.vue'
</script>

<!-- 

States needed:
- current time
- break
- playState (play, pause, restart etc)

-->

<template>
  <header>
    <h1 class="title">Pomodoro Clock</h1>
    <h2 class="subtitle text-color-mute">aka the 25 + 5 clock!</h2>
  </header>
  <div class="main-wrapper">
    <ClockEyebrow>
      <template #heading>Break Length</template>
    </ClockEyebrow>
    <ClockEyebrow>
      <template #heading>Session Length</template>
    </ClockEyebrow>
  </div>
</template>

<style scoped>
.header {
  display: flex;
  width: 100%;
}

.title {
  font-size: 4rem;
  line-height: 1.1;
  text-align: center;
}

.subtitle {
  font-size: 1.25rem;
  text-align: center;
}

.main-wrapper {
  display: flex;
  justify-content: space-between;
  font-size: 1.25rem;
}

</style>
