<template>
  <div>
    <div class="work">
      <header class="work__header" ref="workHeader">
        <div class="work__header-holder" ref="workHolder">
          <img class="work__header-image" :src="imagePath" />
        </div>
      </header>

      <div class="work__meta" ref="meta">
        <ul>
          <li v-for="(meta, index) in item.meta" v-bind:key="index">
            <span class="work__meta-handle">{{ capitlize(index) }}</span>
            {{ meta }}
          </li>

          <li v-for="(meta, index) in item.links" v-bind:key="index">
            <a class="work__meta-handle" :href="meta" target="_blank">{{ capitlize(index) }}</a>
          </li>
        </ul>
      </div>

      <div class="work__content" ref="content">
        <h2 class="work__content-title">{{ this.item.title }}</h2>
        <p class="work__content-text">{{ item.description }}</p>
      </div>
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
  max-width: 70rem;
  margin: 0 auto;
  margin-top: 5rem;
  display: grid;
  grid-template-areas:
    'header'
    'meta'
    'content'
    'footer';
  padding: 0 2rem;
  grid-row-gap: 2em;

  @media screen and (min-width: 40rem) {
    padding: 0 2rem;
    grid-template-areas:
      'header header header '
      'meta content content'
      'footer footer footer';
    grid-column-gap: 8em;
    grid-row-gap: 5em;
  }

  &__header {
    grid-area: header;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    max-height: 50vh;
    overflow: hidden;

    &-holder {
      overflow: hidden;
      opacity: 0;
      clip-path: polygon(0 100%, 100% 100%, 100% 100%, 0% 100%);
    }

    &-image {
      max-width: 100%;
    }
  }

  &__content {
    &-text {
      color: $color-white;
      text-align: left;
    }
  }

  &__meta {
    color: $color-white;
    grid-area: meta;
    margin-top: 0.5rem;
    position: relative;

    li {
      margin-bottom: 0.2rem;
    }

    &-handle {
      font-weight: bold;
      font-size: 1rem;
      letter-spacing: 0;
    }

    a {
      text-decoration: underline;
    }

    @media screen and (min-width: 40rem) {
      margin-top: 4rem;
    }
  }

  &__footer {
    grid-area: footer;
    width: 100%;
    height: 200px;
    background-color: blue;
  }

  &__back {
    height: 10rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>