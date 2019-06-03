<template>
  <div class="work-single" ref="workItem">
    <div class="work-single__image">
      <img :src="image" v-bind:alt="image">
    </div>

    <div class="work-single__content">
      <span class="work-single__content-index">0{{ index }}</span>
      <h2>{{ title }}</h2>
      <p>{{ description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title', 'image', 'description', 'index'],
  // mounted() {
  //   this.$refs.singleWorkItem.addEventListener('scroll', e => {
  //     console.log(e)
  //   })
  // }
  mounted() {
    // Activate scroll
    this.onScroll()
  },
  methods: {
    onScroll() {
      // Get middle point
      let middleOfView = window.innerHeight

      window.onscroll = () => {
        var rect = this.$refs.workItem.getBoundingClientRect()
        if (
          rect.bottom < 0 ||
          rect.right < 0 ||
          rect.left > window.innerWidth ||
          rect.top > window.innerHeight
        ) {
          // console.log('El in not in view')
        } else {
          //    console.log('In view')
        }

        if (Math.floor(rect.top / 2) < middleOfView / 2) {
          console.log('Middle hitted')
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.work-single {
  display: flex;
  margin: 0 auto;
  margin-bottom: 10rem;
  height: 20rem;
  z-index: 9;
  &::last-of-type {
    margin-bottom: 0;
  }
  &__image {
    width: 20rem;
    height: 100%;
    background-color: #a4f6fe;
  }
  &__content {
    transform: translateX(-2rem);
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 20rem;
    height: 100%;
    padding-left: 1rem;
    position: relative;

    &-index {
      position: absolute;
      right: 0;
      top: 0;
      color: #fff;
    }

    h2 {
      line-height: 5rem;
      font-size: 8rem;
      margin-bottom: 3rem;
      color: #fff;
    }

    p {
      color: #fff;
    }
  }
}
</style>