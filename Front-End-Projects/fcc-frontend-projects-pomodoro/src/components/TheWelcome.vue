<script setup>
import ClockEyebrow from './ClockEyebrows.vue'
</script>

<template>
  <div class="main-wrapper">
    <ClockEyebrow>
      <template #heading>Break Length</template>
    </ClockEyebrow>
    <ClockEyebrow>
      <template #heading>Session Length</template>
    </ClockEyebrow>
  </div>
</template>


<!--   
<WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>Documentation</template>

    Vue’s
    <a href="https://vuejs.org/" target="_blank" rel="noopener">official documentation</a>
    provides you with all information you need to get started.
  </WelcomeItem>
  -->