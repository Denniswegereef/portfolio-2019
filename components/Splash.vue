<template>
  <div class="splash">
    <div class="splash__content">
      <h1 class="splash__content-title">Hello I',m</h1>
      <div class="splash__image"></div>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.splash {
  height: 100vh;
  width: 100%;

  &__image {
    height: 500px;
    width: 250px;
    background-color: blue;
    position: absolute;
    z-index: 2;
  }

  &__content {
    bottom: 0;
    background-color: grey;
    &-title {
      color: red;
      &:nth-of-type(1) {
        color: blue;
        z-index: 1;
      }
      &:nth-of-type(2) {
        color: yellow;
        z-index: 3;
      }
      &:nth-of-type(3) {
        color: green;
        z-index: 3;
      }
    }
  }
}
</style>
