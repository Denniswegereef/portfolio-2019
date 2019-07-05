<template>
  <div>
    <div class="work">
      <header class="work__header" ref="workHeader">
        <div class="work__header-holder" ref="workHolder">
          <img class="work__header-image" :src="imagePath" />
        </div>
      </header>

      <div class="work__meta">
        <ul>
          <li>
            <span>Date</span>
            {{ item.date }}
          </li>
          <li>
            <span>Client</span>
            {{ item.client }}
          </li>
          <li>
            <span>Role</span>
            {{ item.role }}
          </li>
          <li>
            <a :href="item.link">
              <span>Online link</span>
            </a>
          </li>
          <li>
            <a :href="item.github">
              <span>Repository</span>
            </a>
          </li>
        </ul>
      </div>

      <div class="work__content">
        <h2>{{ this.item.title }}</h2>
        <p>{{ item.description }}</p>
      </div>
    </div>

    <div class="work__back">
      <nuxt-link to="/">Go back to the home</nuxt-link>
    </div>
    <Footer />
  </div>
</template>

<script>
import workData from '~/static/work.json'
import Footer from '~/components/Footer.vue'

export default {
  workData,
  components: {
    Footer
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
    // TweenMax.to(this.$refs.workHolder.$el, 0.8, {
    //   delay: 0.3,
    //   opacity: 1,
    //   clipPath: '0% 0%, 100% 0%, 100% 100%, 0% 100%'
    // })
    this.showItem()
  },
  methods: {
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
      TweenMax.to('.work__header-holder', 1.2, {
        delay: 0.5,
        opacity: 1,
        clipPath: '0% 0%, 100% 0%, 100% 100%, 0% 100%'
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

  &__meta {
    color: $color-white;
    grid-area: meta;
    margin-top: 0.5rem;

    ul {
      padding: 0;
      list-style-type: none;
    }

    span {
      font-weight: bold;
    }
    @media screen and (min-width: 40rem) {
      margin-top: 2rem;
    }
  }

  &__footer {
    grid-area: footer;
    width: 100%;
    height: 200px;
    background-color: blue;
  }

  &__back {
    height: 20rem;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>