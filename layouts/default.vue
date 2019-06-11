<template>
  <div>
    <div class="about__socials">
      <Socials/>
    </div>

    <nuxt-link to="about" class="about__link">About me</nuxt-link>
    <nuxt/>
  </div>
</template>


<script>
import Socials from '~/components/layout/Socials.vue'
import { TimelineMax } from 'gsap'

export default {
  components: {
    Socials
  }
}
</script>

<style lang="scss">
@import '~assets/css/config';

html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

body {
  background-color: $color-grey-dark;
}

.about {
  &__socials {
    position: fixed;
    bottom: 1rem;
    left: 1rem;
  }
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
