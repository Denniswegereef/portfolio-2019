<template>
  <div>
    <!-- <div class="fullscreen" ref="fullscreen"></div> -->
    <section class="splash-holder"></section>

    <section class="splash">
      <div class="splash__container" ref="container" :class="onTop ? '' :  'active'">
        <h1 class="splash__title-first" ref="first">Dennis</h1>
        <div class="splash__title-image-holder" ref="image">
          <img class="splash__title-image-holder__image" src="~/static/images/me.png" alt="me.png" />
        </div>
        <h1 class="splash__title-second" ref="second">Wegereef</h1>
        <h2 class="splash__title-extra" ref="extra">
          Front end developer
          <br />Looking for a intership
        </h2>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      onTop: true,
      showExtra: false
    }
  },

  mounted() {
    console.log(window)
    this.fullScreen()
    // Activate scroll
    this.onScroll()
    this.onMouseMove(window)
    this.checkPositionPage()

    this.introAnimation()
  },
  methods: {
    introAnimation() {
      TweenMax.to(this.$refs.image, 0.8, {
        clipPath: '0% 0%, 100% 0%, 100% 100%, 0% 100%',
        opacity: 1,
        delay: 1.6
      })

      TweenMax.from(this.$refs.first, 1.5, {
        opacity: 0,
        y: '-20',
        delay: 0.5
      })

      TweenMax.from(this.$refs.second, 1.5, {
        opacity: 0,
        y: '20',
        delay: 1
      })

      TweenMax.from(this.$refs.extra, 2, {
        opacity: 0,
        delay: 2.5,
        onComplete: () => {
          this.showExtra = true
        }
      })
    },
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

      TweenMax.to(this.$refs.first, 2, {
        rotationY: -0.04 * sxPos,
        rotationX: 0.04 * syPos,
        transformPerspective: 500,
        transformOrigin: 'center center -400',
        ease: Expo.easeOut
      })

      TweenMax.to(this.$refs.image, 2, {
        rotationY: -0.058 * sxPos,
        rotationX: 0.058 * syPos,
        transformPerspective: 500,
        transformOrigin: 'center center -400',
        ease: Expo.easeOut
      })

      TweenMax.to(this.$refs.second, 2, {
        rotationY: -0.068 * sxPos,
        rotationX: 0.068 * syPos,
        transformPerspective: 500,
        transformOrigin: 'center center -400',
        ease: Expo.easeOut
      })

      TweenMax.to(this.$refs.extra, 2, {
        rotationY: -0.078 * sxPos,
        rotationX: 0.078 * syPos,
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
        TweenMax.to(this.$refs.container, 0.5, {
          opacity: 1
        })
        if (this.showExtra) {
          TweenMax.to(this.$refs.extra, 0.5, {
            opacity: 1
          })
        }
      } else {
        TweenMax.to(this.$refs.container, 0.5, {
          opacity: 0.05
        })
        if (this.showExtra) {
          TweenMax.to(this.$refs.extra, 0.5, {
            opacity: 0
          })
        }
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

.splash-holder {
  height: 100vh;
  width: 100%;
}

.splash {
  position: fixed;
  width: 100%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  &__container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    z-index: -1;
    position: relative;
  }
  &__title {
    &-first,
    &-second {
      @media screen and (min-width: 40rem) {
        font-size: 10vw;
        line-height: 6vw;
        z-index: -4;
        font-family: $font-headings;
      }
    }
    &-first {
      z-index: -5;
    }

    &-second {
      z-index: -1;
    }

    &-image-holder {
      position: absolute;
      z-index: -4;
      height: 4rem;
      width: 6rem;
      top: -6rem;
      display: flex;
      align-content: center;
      justify-content: center;
      box-shadow: 0px 3px 15px rgba(0, 0, 0, 0.2);
      clip-path: polygon(0% 100%, 100% 100%, 100% 100%, 0% 100%);

      &__image {
        height: 100%;
      }

      @media screen and (min-width: 40rem) {
        top: 20%;
        height: 8vw;
        width: 12vw;
      }
    }

    &-extra {
      font-family: $font-body;
      letter-spacing: 2px;
      font-size: 1.1rem;
      line-height: 1rem;
      text-align: center;

      @media screen and (min-width: 40rem) {
        transform: translateX(50%);
        font-size: 2vw;
        line-height: 2vw;
        text-align: left;
      }
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

.show {
  .splash__title-image-holder {
    clip-path: polygon(
      50% 0%,
      90% 20%,
      100% 60%,
      75% 100%,
      25% 100%,
      0% 60%,
      10% 20%
    );
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
