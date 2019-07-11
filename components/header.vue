<template>
  <div class="heading">
    <div class="heading__main" ref="first">
      <slot />
    </div>
    <div class="heading__second" ref="second">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    TweenMax.from(this.$refs.second, 0.6, {
      y: 50,
      opacity: 0,
      delay: 1
    })
  }
}
</script>

<style lang="scss" scoped>
.heading {
  position: relative;
  overflow: hidden;
  &__main {
    opacity: 0;
  }
  &__second {
    position: absolute;
    top: 0;
    left: 0;
  }

  h2 {
    margin: 0;
  }
}
</style>