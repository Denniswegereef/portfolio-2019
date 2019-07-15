<template>
  <div class="work__container">
    <div class="work">
      <header class="work__header" ref="workHeader">
        <div class="work__header-holder" ref="workHolder">
          <img class="work__header-image" :src="imagePath" />
        </div>

        <h2 class="work__header-title" ref="title">{{ this.item.title }}</h2>
      </header>

      <main class="work__info">
        <div class="work__meta" ref="meta">
          <ul>
            <li v-for="(meta, index) in item.meta" v-bind:key="index">
              <p>
                <span class="work__meta-handle">{{ capitlize(index) }}:</span>
                {{ meta }}
              </p>
            </li>

            <li v-for="(meta, index) in item.links" v-bind:key="index">
              <a class="work__meta-handle" :href="meta" target="_blank">{{ capitlize(index) }}</a>
            </li>
          </ul>
        </div>

        <div class="work__content" ref="content">
          <p
            class="work__content-text"
            v-for="(paragraph, index) in item.description"
            v-bind:key="index"
          >{{ paragraph }}</p>
        </div>
      </main>
    </div>

    <div class="work__back">
      <nuxt-link to="/">Go back to the home</nuxt-link>
    </div>
    <!-- <Footer /> -->
  </div>
</template>

<script>
import workData from '~/static/work.json'
import Footer from '~/components/Footer.vue'
import Header from '~/components/header.vue'

export default {
  workData,
  components: {
    Footer,
    Header
  },
  head() {
    return {
      title: this.item.title
    }
  },
  data() {
    return {
      id: this.$route.params.item
    }
  },
  validate({ params }) {
    if (workData.find(item => item.id === params.item)) {
      return true
    }
  },
  mounted() {
    this.onMouseMove(window)
    console.log(this.$refs.workHolder)
    this.showItem()
  },
  methods: {
    capitlize(metaTag) {
      return (
        metaTag.charAt(0).toUpperCase() + metaTag.slice(1).replace('-', ' ')
      )
    },
    onMouseMove(window) {
      TweenMax.set(this.$refs.workHeader, { transformStyle: 'preserve-3d' })

      window.addEventListener('mousemove', this.tilt)
    },
    tilt(e) {
      const body = document.body.getBoundingClientRect()
      const sxPos = ((e.pageX / body.width) * 100 - 50) * 2
      const syPos = ((e.pageY / body.height) * 100 - 50) * 2

      TweenMax.to(this.$refs.workHeader, 2, {
        rotationY: -0.02 * sxPos,
        rotationX: 0.02 * syPos,
        transformPerspective: 500,
        transformOrigin: 'center center -400',
        ease: Expo.easeOut
      })
    },
    showItem() {
      TweenMax.to('.work__header-holder', 0.8, {
        delay: 0.5,
        opacity: 1,
        clipPath: '0% 0%, 100% 0%, 100% 100%, 0% 100%'
      })

      TweenMax.from(this.$refs.content, 0.5, {
        delay: 1.2,
        opacity: 0,
        y: 20
      })

      TweenMax.from(this.$refs.title, 1, {
        delay: 1,
        opacity: 0,
        x: -20
      })

      TweenMax.from(this.$refs.meta, 0.5, {
        delay: 1.7,
        opacity: 0,
        x: -20
      })
    }
  },
  computed: {
    item() {
      return workData.find(item => item.id === this.id)
    },
    imagePath() {
      return require(`~/static/images/${this.item.image}`)
    }
  },
  beforeDestroy() {
    window.removeEventListener('mousemove', this.tilt)
  },
  layout: 'Default'
}
</script>

<style lang="scss" scoped>
@import '~assets/css/config';

.work {
  &__container {
    margin-top: 3rem;
    padding: 1.5rem;
    @media screen and (min-width: 40rem) {
      padding: 0rem;
      margin-top: 6rem;
    }
  }
  &__header {
    max-width: 55rem;
    margin: 0 auto;
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 2rem;
    @media screen and (min-width: 40rem) {
      align-items: flex-end;
      flex-direction: row;
      margin-bottom: 6rem;
    }
    &-holder {
      width: 100%;
      margin-bottom: 1rem;
      @media screen and (min-width: 40rem) {
        margin-bottom: 0rem;
        width: 70%;
        clip-path: polygon(0 100%, 100% 100%, 100% 100%, 0 100%);
      }
    }
    &-image {
      width: 100%;
    }
    &-title {
      margin-bottom: 0;
      @media screen and (min-width: 40rem) {
        margin-left: 1rem;
      }
    }
  }

  &__info {
    max-width: 50rem;
    display: flex;
    flex-direction: column;
    margin: 0 auto;
    @media screen and (min-width: 50rem) {
      flex-direction: row;
    }
  }

  &__meta {
    text-align: left;
    min-width: 14rem;
    margin-bottom: 1rem;
    p {
      font-size: 1rem;
      margin-bottom: 0;
    }
    li {
      color: $color-white;
      margin-bottom: 0.4rem;
    }
    a {
      text-decoration: underline;
    }
    span {
      font-weight: bold;
    }
    @media screen and (min-width: 50rem) {
      margin-right: 2rem;
      text-align: right;
      margin-bottom: 0rem;
    }
  }

  &__content {
    width: 100%;
  }

  &__back {
    height: 16rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>