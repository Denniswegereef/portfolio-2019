<template>
  <nuxt-link :to="'work/' + id" class="work-single" ref="workItem" :class="oddEven">
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
      show: false
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
        threshold: 0.8
      }
    )

    console.log(this.$refs.workContent.children)

    this.observer.observe(this.$refs.workItem.$el)
  },
  computed: {
    oddEven() {
      return this.$props.index % 2 ? 'work-single__even' : 'work-single__odd'
    }
  },
  methods: {
    inView() {
      this.show = true
      if (this.show) {
        console.log('inview')
      }
    },
    showItem() {
      TweenMax.to(this.$refs.workHolder, 0.8, {
        delay: 0.3,
        opacity: 1,
        clipPath: '0% 0%, 100% 0%, 100% 100%, 0% 100%'
      })
      TweenMax.staggerFrom(
        this.$refs.workContent.children,
        0.5,
        { opacity: 1, y: 0 },
        0.05
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
  align-items: center;
  cursor: pointer;

  @media screen and (min-width: 40rem) {
    flex-direction: row;
    max-width: 50rem;
    margin-bottom: 10rem;
  }
  &:hover {
    .work-single__image {
      transform: scale(1.1);
    }
  }

  &__title {
    width: 100%;
    margin-bottom: 0.2rem;
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
      transition: transform 0.3s;
    }
  }

  &__holder {
    width: 100%;
    overflow: hidden;
    opacity: 0;
    clip-path: polygon(0 100%, 100% 100%, 100% 100%, 0% 100%);
  }

  &__image {
    transition: transform 1s;
    width: 100%;
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