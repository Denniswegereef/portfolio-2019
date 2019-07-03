<template>
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
</template>

<script>
export default {
  data() {
    return {
      onTop: true
    }
  },

  mounted() {
    // Activate scroll
    this.onScroll()
    this.onMouseMove(window)
    this.checkPositionPage()
  },
  methods: {
    onMouseMove(window) {
      TweenMax.set(this.$refs.container, { transformStyle: 'preserve-3d' })

      window.addEventListener('mousemove', e => {
        this.tilt(e.pageX, e.pageY)
      })
    },
    tilt(cx, cy) {
      const body = document.body.getBoundingClientRect()
      const sxPos = ((cx / body.width) * 100 - 50) * 2
      const syPos = ((cy / body.height) * 100 - 50) * 2

      TweenMax.to(this.$refs.container, 2, {
        rotationY: -0.04 * sxPos,
        rotationX: 0.04 * syPos,
        transformPerspective: 500,
        transformOrigin: 'center center -400',
        ease: Expo.easeOut
      })
    },
    onScroll() {
      // Get middle point
      window.onscroll = () => {
        this.checkPositionPage()
      }
    },
    checkPositionPage() {
      window.scrollY === 0 ? (this.onTop = true) : (this.onTop = false)
    }
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
      color: #fff;
    }
    &-second {
      font-family: $font-body;
      letter-spacing: 2px;
      transition: color 0.3, opacity 0.2s;
      margin: 0;
    }
  }
  .active {
    .splash__title {
      &-first {
        opacity: 0.02;
        transform: translateY(2rem);
      }
      &-second {
        opacity: 0;
        color: lighten($color-grey-dark, 5%);
      }
    }
  }
}
</style>
