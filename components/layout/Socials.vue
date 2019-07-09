<template>
  <ul class="socials">
    <a
      class="socials__item"
      ref="items"
      v-for="(item, index) in socials"
      v-bind:key="index"
      href="item.link"
      target="_blank"
    >{{ item.name}}</a>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      socials: [
        {
          name: 'Instagram',
          link: 'httpL//www.asldjf'
        },
        {
          name: 'Github',
          link: 'httpL//www.asldjf'
        },
        {
          name: 'Facebook',
          link: 'httpL//www.asldjf'
        }
      ]
    }
  },
  mounted() {
    TweenMax.staggerFrom(
      this.$refs.items,
      1.2,
      { x: '-20', opacity: 0, delay: 1.5 },
      0.4
    )

    console.log(this.$refs.items)
  }
}
</script>

<style lang="scss" styled>
@import '~assets/css/config';

.socials {
  position: fixed;
  left: 1.5rem;
  bottom: 1rem;
  display: flex;
  flex-direction: column;
  list-style-type: none;
  padding: 0;
  &__item {
    color: $color-white;
  }
}
</style>