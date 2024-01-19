<template lang="pug">
.background-element
  img(src="/images/bg-element-1.svg" alt="")
  img(src="/images/bg-element-2.svg" alt="")
  img(src="/images/bg-element-3.svg" alt="")
  img(src="/images/bg-element-4.svg" alt="")
  img(src="/images/bg-element-5.svg" alt="")
</template>

<script>
</script>

<style lang="scss" scoped>
.background-element {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 1px;
  height: 1px;
  @media (max-width: 1480px) {
    display: none;
  }
  img:nth-child(1){
    position: absolute;
    left: -784px;
    top: -328px;
  }
  img:nth-child(2){
    position: absolute;
    left: -826px;
    top: 36px;
  }
  img:nth-child(3){
    position: absolute;
    right: -934px;
    top: -206px;
  }
  img:nth-child(4){
    position: absolute;
    top: 359px;
    right: -809px;
  }
  img:nth-child(5){
    position: absolute;
    top: 369px;
    right: -859px;
  }
}

</style>