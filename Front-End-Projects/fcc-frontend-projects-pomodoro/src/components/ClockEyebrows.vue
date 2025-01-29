<template>
  <div class="eyebrow">
    <div class="eyebrow_top">
      <h3>
        <slot name="heading"></slot>
      </h3>
    </div>
    <div class="eyebrow_bottom">
      <div class="icon-arrow icon-arrow--down effect-hover-pointer">←</div>
      <div class="eyebrow_display">
        <slot name="display">0</slot>
      </div>
      <div class="icon-arrow icon-arrow--up effect-hover-pointer">→</div>
    </div>
  </div>
</template>

<style scoped>

.eyebrow_top h3 {
  font-weight: 500;
  text-align: center;
}
.eyebrow_bottom {
    display: flex;
    width: 100%;
    justify-content: space-around;
    align-items: center;
}

.icon-arrow {
  font-size: 2rem;
  transform: rotate(-90deg);
}
</style>
