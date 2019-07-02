<template>
  <nuxt-link :to="correctPath" class="about__link">{{go}}</nuxt-link>
</template>

<script>
export default {
  props: {
    go: {
      default: 'Go back',
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
    color: $color-white;
    &:hover {
      color: $color-primary;
    }
  }
}
</style>
