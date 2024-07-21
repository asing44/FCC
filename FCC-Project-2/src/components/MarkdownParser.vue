<script setup lang="ts">
  import { ref } from 'vue';
  import { marked } from 'marked';

const text = ref("");

marked.setOptions({
  renderer: new marked.Renderer(),
  gfm: true,
  tables: true,
  breaks: true,
  pedantic: false,
  sanitize: false,
  smartLists: true,
  smartypants: false
});

</script>

<template>
  <div class="container">
    <input class="input" type="input" placeholder="Enter Markdown here..." v-model="text" />
    <div class="output" v-html=" marked(text) "></div>
  </div>
</template>

<style>
.output {
  border: 1px solid #ddd;
  padding: 10px;
  margin-top: 10px;
  text-align: left;
}

.input {
  width: 100%;
  height: 150px;
}
</style>
