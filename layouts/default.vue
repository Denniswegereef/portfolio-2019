<template>
  <div>
    <div class="fullscreen" v-if="loaded"></div>
    <AboutSwitch />
    <nuxt />
    <Socials />
  </div>
</template>


<script>
import Socials from '~/components/layout/Socials.vue'
import AboutSwitch from '~/components/layout/AboutSwitch.vue'

import { TimelineMax } from 'gsap'
import { setTimeout } from 'timers'

export default {
  components: {
    Socials,
    AboutSwitch
  },
  data() {
    return {
      loaded: false
    }
  }
}
</script>

<style lang="scss">
@import '~assets/css/config';

.fullscreen {
  height: 100vh;
  width: 100%;
  background-color: grey;
  position: fixed;
  z-index: 9999;
  top: 0;
  left: 0;
}
</style>
