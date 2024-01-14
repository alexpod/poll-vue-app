<script setup>
</script>

<template lang="pug">
.window
  .window__header
    .window__header-dots
  .window__content
    slot
</template>

<style lang="scss" scoped>
.window {
  background-color: #fff;
  border-radius: 20px;
  width: 1449px;
  min-height: 880px;
  @media (max-width: 576px) {
    border-radius: 0;
  }
  &__header {
    height: 39px;
    background: var(--Gray-1, #F7F7F9);
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
    display: flex;
    align-items: center;
    @media (max-width: 576px) {
      display: none;
    }
    &-dots {
      width: 9px;
      height: 9px;
      background-color: #D6101F;
      border-radius: 50%;
      position: relative;
      margin-left: 27px;
      &::before {
        content: '';
        width: 9px;
        height: 9px;
        border-radius: 50%;
        background-color: #FFC700;
        position: absolute;
        left: 18px;
      }
      &::after {
        content: '';
        width: 9px;
        height: 9px;
        border-radius: 50%;
        background-color: #85D403;
        position: absolute;
        left: 36px;
      }
    }
  }
  &__content {
    // padding: 269px 40px 50px 100px;
    padding: 40px 40px 50px 100px;
    position: relative;
    color: #000;
    @media (max-width: 576px) {
      padding: 20px;
    }
  }
}
</style>