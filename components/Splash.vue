<template>
  <section class="splash">
    <div class="splash__container">
      <h1 class="splash__title-first">
        Hi, Dennis Wegereef
        <br>a front-end based in Amsterdam
      </h1>
      <h2 class="splash__title-second">Looking for an internship</h2>
    </div>
  </section>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
@import '~assets/css/config';

.splash {
  height: 100vh;
  width: 100%;
  &__container {
    padding: 0 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    height: inherit;
    width: inherit;
  }
  &__title {
    &-first {
      text-align: center;
    }
    &-second {
      margin: 0;
    }
  }
}
</style>
