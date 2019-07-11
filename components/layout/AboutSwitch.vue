<template>
  <div class="layout-header">
    <nuxt-link :to="aboutLink" class="layout-header__links" ref="links">{{ this.aboutText }}</nuxt-link>
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
  data() {
    return {
      aboutText: '',
      aboutLink: ''
    }
  },
  mounted() {
    TweenMax.from(this.$refs.links.$el, 1.2, {
      opacity: 0,
      y: -20,
      delay: 1.5
    })
    this.changeName(this.$route)
  },
  watch: {
    $route(to, from) {
      this.changeName(to)
    }
  },
  methods: {
    changeName(router) {
      if (router.path === '/about') {
        this.aboutText = 'Go back'
        this.aboutLink = '/'
      } else {
        this.aboutText = 'About Dennis'
        this.aboutLink = '/about'
      }
    }
  }
}
</script>
<style lang="scss" scoped>
@import '~assets/css/config';

.layout-header {
  &__links {
    color: #fff;
    font-size: 1.3rem;
    position: fixed;
    top: 1.8rem;
    right: 1.8rem;
    z-index: 999;
    &:hover {
      text-decoration: underline;
    }
  }
  @media screen and (min-width: 40rem) {
    display: flex;
  }
}
</style>
