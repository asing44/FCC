<script setup lang="ts">
import MarkdownParser from './components/MarkdownParser.vue'
</script>

<template>
  <main class="main-block">
    <h1 class="h1">Markdown Parser!</h1>
    <h2 class="h2">Paste your Markdown into the input below!</h2>
    <div id="app">
      <MarkdownParser />
    </div>
  </main>
</template>

<style scoped>

#app {
  display: flex;
  width: 100%;
  margin: 60px 0 0 0;
  padding: 0;
  color: white;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}

.h2 {
  margin-top: 24px;
}

.main-block {
  display: flex;
  justify-content: left;
  align-items: flex-start;
  flex-direction: column;
}


.container, .width  {
  width: 100%;
}

</style>