<template>
  <nuxt-link
    to="#"
    @click.native="goPage(`work/${id}`)"
    class="work-single"
    ref="workItem"
    :class="oddEven"
  >
    <div class="work-single__holder" ref="workHolder">
      <img class="work-single__image" :src="`images/${image}`" />
    </div>

    <div class="work-single__content" ref="workContent">
      <h2 class="work-single__title">{{ title }}</h2>
      <p>Read more</p>
    </div>
  </nuxt-link>
</template>

<script>
import Header from '~/components/header.vue'

export default {
  props: {
    title: {
      type: String,
      default: 'No title found',
      required: true
    },
    image: {
      type: String,
      default: 'placeholder.png',
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      observer: null,
      show: false,
      clicked: false
    }
  },
  mounted() {
    this.observer = new IntersectionObserver(
      (entry, observer) => {
        if (entry[0].intersectionRatio > 0 && !this.show) {
          this.show = true
          this.showItem()
        }
      },
      {
        threshold: 0
      }
    )
    this.observer.observe(this.$refs.workItem.$el)
  },
  computed: {
    oddEven() {
      return this.$props.index % 2 ? 'work-single__even' : 'work-single__odd'
    }
  },
  methods: {
    goPage(param) {
      if (!this.clicked) {
        TweenMax.to('.work-single__holder', 0.6, {
          opacity: 0,
          y: -20,
          onComplete: () => this.pushRouter(param)
        })

        TweenMax.to('.work-single__content', 0.5, {
          delay: 0.1,
          opacity: 0,
          y: -60
        })

        TweenMax.to('.splash', 0.3, {
          delay: 0.2,
          opacity: 0
        })
      }
      this.clicked = true
    },
    pushRouter(param) {
      this.$router.push(param)
    },
    inView() {
      this.show = true
      if (this.show) {
        console.log('inview')
      }
    },
    showItem() {
      const tl = new TimelineMax()

      tl.set(this.$refs.workContent, {
        opacity: 0,
        y: 40
      })
        .to(this.$refs.workHolder, 0.5, {
          delay: 0.3,
          opacity: 1,
          clipPath: '20% 0%, 80% 0%, 80% 100%, 20% 100%'
        })
        .to(this.$refs.workHolder, 0.5, {
          delay: 0.1,
          clipPath: '0% 0%, 100% 0%, 100% 100%, 0% 100%'
        })
        .to(
          this.$refs.workContent,
          1,
          {
            y: 0,
            ease: Power3.easeOut
          },
          '-=0.4'
        )
        .to(
          this.$refs.workContent,
          0.6,
          {
            opacity: 1,
            ease: Power2.easeNone
          },
          '-=0.8'
        )
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~assets/css/config';

$titlePadding: 1rem;

.work-single {
  margin-bottom: 5rem;
  display: flex;
  align-self: flex-end;
  flex-direction: column;
  align-items: baseline;
  cursor: pointer;

  @media screen and (min-width: 40rem) {
    flex-direction: row;
    align-items: center;
    max-width: 50rem;
    margin-bottom: 10rem;
  }
  &:hover {
    .work-single__image {
      transform: scale(1.1);
      filter: grayscale(0%);
    }
  }

  &__title {
    width: 100%;
    margin-bottom: 0.2rem;
    color: $color-white;
    transition: transform 0.3s;

    @media screen and (min-width: 40rem) {
      margin-bottom: 1rem;
      width: auto;
    }
  }

  &__content {
    font-size: 0.9rem;

    @media screen and (min-width: 40rem) {
      font-size: 1.2rem;
    }

    p {
      color: $color-white;
      transition: transform 0.3s;
    }
  }

  &__holder {
    width: 100%;
    overflow: hidden;
    opacity: 0;
    clip-path: polygon(20% 100%, 80% 100%, 80% 100%, 20% 100%);
  }

  &__image {
    transition: transform 1s, filter 0.5s;
    width: 100%;
    filter: grayscale(50%);
  }

  &__odd {
    @media screen and (min-width: 40rem) {
      display: flex;
      flex-direction: row-reverse;
      .work-single__title,
      p {
        text-align: right;
        margin-right: $titlePadding;
      }
    }
    &:hover {
      @media screen and (min-width: 40rem) {
        p {
          transform: translateX(-1rem);
        }
      }
    }
  }

  &__even {
    @media screen and (min-width: 40rem) {
      display: flex;
      .work-single__title,
      p {
        text-align: left;
        margin-left: $titlePadding;
      }
    }
    &:hover {
      @media screen and (min-width: 40rem) {
        p {
          transform: translateX(1rem);
        }
      }
    }
  }
}
</style>