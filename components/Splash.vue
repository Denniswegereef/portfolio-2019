<template>
  <div>
    <div class="fullscreen" ref="fullscreen"></div>

    <section class="splash">
      <div class="splash__container" ref="container" :class="onTop ? '' :  'active'">
        <h1 class="splash__title-first">
          Dennis Wegereef
          <br />a front-end developer
          <br />based in Amsterdam
        </h1>
        <h3 class="splash__title-second">Looking for an internship</h3>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      onTop: true
    }
  },

  mounted() {
    this.fullScreen()
    // Activate scroll
    this.onScroll()
    this.onMouseMove(window)
    this.checkPositionPage()
  },
  methods: {
    fullScreen() {
      // TweenMax.to(this.$refs.fullScreen, 0.5, {
      //   opaciity: 0
      //   //onComplete: this.$refs.fullScreen.$el.remove()
      // })
    },
    onMouseMove(window) {
      TweenMax.set(this.$refs.container, { transformStyle: 'preserve-3d' })

      window.addEventListener('mousemove', this.tilt)
    },
    tilt(e) {
      const body = document.body.getBoundingClientRect()
      const sxPos = ((e.pageX / body.width) * 100 - 50) * 2
      const syPos = ((e.pageY / body.height) * 100 - 50) * 2

      TweenMax.to(this.$refs.container, 2, {
        rotationY: -0.04 * sxPos,
        rotationX: 0.04 * syPos,
        transformPerspective: 500,
        transformOrigin: 'center center -400',
        ease: Expo.easeOut
      })
    },
    onScroll() {
      window.onscroll = this.checkPositionPage
    },
    checkPositionPage() {
      if (window.scrollY === 0) {
        this.onTop = true
      } else {
        this.onTop = false
      }
    }
  },
  beforeDestroy() {
    window.removeEventListener('mousemove', this.tilt)
  }
}
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
    position: fixed;
    z-index: -1;
  }
  &__title {
    &-first {
      text-transform: uppercase;
      transition: opacity 0.3s, transform 0.2s ease-out;
      text-align: center;
      color: $color-primary;
    }
    &-second {
      font-family: $font-body;
      letter-spacing: 2px;
      transition: color 0.3, opacity 0.2s;
      margin: 0;
      color: $color-black;
    }
  }
  .active {
    .splash__title {
      &-first {
        opacity: 0.2;
        color: grey;
        transform: translateY(2rem);
      }
      &-second {
        opacity: 0;
        color: lighten($color-grey-dark, 5%);
      }
    }
  }
}

// .fullscreen {
//   height: 100vh;
//   width: 100%;
//   position: fixed;
//   background-color: red;
//   top: 0;
//   left: 0;
//   z-index: 999;
// }
</style>
