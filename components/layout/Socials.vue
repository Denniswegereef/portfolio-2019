<template>
  <ul class="socials" v-if="show">
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
      show: true,
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
    this.hideShow(this.$router)
  },
  watch: {
    $route(to, from) {
      this.hideShow(to)
    }
  },
  methods: {
    hideShow(router) {
      if (router.path === '/about') {
        this.show = false
      } else {
        this.show = true
      }
    }
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
  display: none;

  &__item {
    color: $color-white;
  }

  @media screen and (min-width: 40rem) {
    display: flex;
  }
}
</style>