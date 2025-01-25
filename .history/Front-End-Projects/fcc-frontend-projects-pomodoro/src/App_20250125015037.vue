<script setup>
import TheWelcome from './components/TheWelcome.vue'
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
    <h2 class="subtitle">aka the 25 + 5 clock!</h2>
  </header>
  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
.header {
  display: flex;
  width: 100%;
}

.subtitle {
  font-size: 1.25rem;
  text-align: center;
}

</style>
