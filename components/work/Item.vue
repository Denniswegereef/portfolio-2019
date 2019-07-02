<template>
  <nuxt-link :to="'work/' + index" class="work-single" ref="workItem" :class="oddEven">
    <div class="work-single__holder">
      <img class="work-single__image" :src="`images/${image}`">
    </div>

    <h1 class="work-single__title">{{ title }}</h1>
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
    }
  },
  computed: {
    oddEven() {
      return this.$props.index % 2 ? 'work-single__even' : 'work-single__odd'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~assets/css/config';

$titlePadding: 2rem;

.work-single {
  margin-bottom: 5rem;
  display: flex;
  align-self: flex-end;
  flex-direction: column;
  align-items: center;
  @media screen and (min-width: 40rem) {
    flex-direction: row;
    max-width: 50rem;
    margin-bottom: 10rem;
  }

  &__title {
    width: 100%;
    @media screen and (min-width: 40rem) {
      width: auto;
    }
  }

  &__holder {
    width: 100%;
    overflow: hidden;
  }

  &__image {
    width: 100%;
  }

  &__odd {
    @media screen and (min-width: 40rem) {
      display: flex;
      flex-direction: row-reverse;
      .work-single__title {
        text-align: right;
        margin-right: $titlePadding;
      }
    }
  }

  &__even {
    @media screen and (min-width: 40rem) {
      display: flex;
      .work-single__title {
        text-align: left;
        margin-left: $titlePadding;
      }
    }
  }
}
</style>