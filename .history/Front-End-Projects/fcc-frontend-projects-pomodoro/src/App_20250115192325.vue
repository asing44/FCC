<script setup>
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <h1>Pomodoro Clock!</h1>
    <h2 class="subheading">aka the 25 + 5 clock!</h2>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
.header {
  text-align: center;
}

.subheading {
  font-size: 1.25rem;
}
</style>
