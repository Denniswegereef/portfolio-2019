<template>
  <div>
    <AboutSwitch />
    <nuxt />
  </div>
</template>


<script>
import Socials from '~/components/layout/Socials.vue'
import AboutSwitch from '~/components/layout/AboutSwitch.vue'

import { TimelineMax } from 'gsap'

export default {
  components: {
    Socials,
    AboutSwitch
  }
}
</script>

<style lang="scss">
@import '~assets/css/config';
</style>
