<template>
  <div>
    <nuxt-link to="/">Home</nuxt-link>
    <nuxt-link :to="correctPath" class="about__link">Go {{go}}</nuxt-link>
  </div>
</template>

<script>
export default {
  props: {
    go: {
      default: 'back',
      type: String
    }
  },
  computed: {
    correctPath() {
      let go = this.$props.go
      return go.toLowerCase() === 'about'
        ? '/' + go.charAt(0).toUpperCase() + go.slice(1)
        : '/'
    }
  }
}
</script>
<style lang="scss" scoped>
@import '~assets/css/config';

.about {
  &__link {
    position: fixed;
    top: 1rem;
    right: 1rem;
    &:hover {
      color: $color-primary;
    }
  }
}
</style>
