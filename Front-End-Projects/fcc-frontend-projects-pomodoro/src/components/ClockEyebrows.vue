<template>
  <div class="eyebrow">
    <div class="eyebrow_top">
      <h3>
        <slot name="heading"></slot>
      </h3>
    </div>
    <div class="eyebrow_bottom">
      <div class="icon-arrow is--left">←</div>
      <div class="eyebrow_display">
        <slot name="display"></slot>
      </div>
      <div class="icon-arrow is--right">→</div>
    </div>
  </div>
</template>

<style scoped>
.eyebrow_top {
  text-align: center;
}
  .eyebrow_bottom {
    display: flex;
    width: 100%;
    justify-content: space-around;
  }
</style>
