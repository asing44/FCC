<template>
  <div class="button-container">
    <button class="button">
      <slot name="button-slot"></slot>
    </button>
    <slot name="audio-slot"></slot>
  </div>
</template>

<style scoped>
.button-container {
  position: relative;
  place-content: center;
  height: 5rem;
  width: 8rem;
}

.button {
  display: block;
  height: 100%;
  width: 100%;
    border: unset;
    border-radius: 1rem;
  box-shadow: 2px 2px 2px 1px gray;
  cursor: pointer;
}

.button:hover {
  background-color: #DCE9F7;
}

@media (min-width: 1024px) {
  
}
</style>
