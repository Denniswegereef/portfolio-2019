<template>
  <div class="work-single" ref="workItem">
    <div class="work-single__holder">
      <img class="work-single__image" :src="image" v-bind:alt="image">
    </div>

    <div class="work-single__content">
      <span class="work-single__index">0{{ index }}</span>
      <h2 class="work-single__title">{{ title }}</h2>
      <div class="work-single__description-holder">
        <p class="work-single__description-view">View more</p>
        <p class="work-single__description-text">{{ description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title', 'image', 'description', 'index'],
  data() {
    return {
      animationFirst: false
    }
  },
  computed: {
    middleOfView() {
      return window.innerHeight
    }
  },
  mounted() {
    // Activate scroll
    this.onScroll()

    // Check once if item is here
    this.checkPosition()
  },
  methods: {
    onScroll() {
      // Get middle point
      window.onscroll = () => {
        this.checkPosition()
      }
    },
    checkPosition() {
      var rect = this.$refs.workItem.getBoundingClientRect()
      if (
        rect.bottom < 0 ||
        rect.right < 0 ||
        rect.left > window.innerWidth ||
        (rect.top > window.innerHeight && this.animationFirst)
      ) {
      } else {
        this.animationFirst = true
        TweenMax.to(this.$refs.workItem, 0.5, {
          y: '100px',
          delay: 1
        })
        this.$refs.workItem
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~assets/css/config';

.work-single {
  display: flex;
  align-items: center;
  margin-bottom: 15rem;
  position: relative;

  &:hover {
    .work-single__content {
      transform: translateX(-2rem);
    }

    .work-single__title {
      -webkit-text-stroke: 2px $color-white;
      color: rgba($color-primary, 0);
    }

    .work-single__holder {
      clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
    }

    .work-single__image {
      filter: hue-rotate(0deg);
      transform: scale(1.1);
    }

    .work-single__description {
      &-holder {
      }
      &-text {
        transform: translateY(200%);
      }
      &-view {
        transform: translateY(200%);
        transform: translateY(0%);
        opacity: 1;
      }
    }
  }

  &__holder {
    width: 30rem;
    height: 25rem;
    transition: clip-path 0.3s ease-in-out;
    clip-path: polygon(5% 5%, 95% 5%, 95% 95%, 5% 95%);
  }
  &__image {
    width: 100%;
    object-fit: cover;
    transition: transform 0.5s, filter 0.7s;
    filter: hue-rotate(90deg);
  }

  &__content {
    transition: transform 0.2s ease-in-out;
    transform: translateX(-10rem);
  }

  &__title {
    margin-bottom: 0;
    letter-spacing: 20;
    -webkit-text-stroke: 2px $color-white;
    color: rgba($color-primary, 0);
  }

  &__description {
    color: $color-white;
    position: relative;
    overflow: hidden;
    &-holder {
      width: 100%;
      height: 2rem;
      overflow: hidden;
    }
    &-text {
      transition: transform 0.4s;
      color: $color-white;
      margin: 0;
    }
    &-view {
      margin: 0;
      color: $color-white;
      position: absolute;
      margin-left: 1rem;
      transform: translateY(-100%);
      transition: transform 0.2s;
      opacity: 0;
      text-transform: uppercase;
      font-weight: bold;
    }
  }
  &__index {
    position: absolute;
    top: 0;
    right: 0;
    color: $color-white;
  }
}
</style>