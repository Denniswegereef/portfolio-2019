<template>
  <ul class="socials">
    <a
      class="socials__item"
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
  }
}
</script>

<style lang="scss" styled>
@import '~assets/css/config';

.socials {
  display: flex;
  color: $color-white;
  list-style-type: none;
  padding-left: 0;
  &__item {
    color: $color-white;
    margin-left: 1rem;
    &:first-of-type {
      margin-left: 0;
    }
  }
}
</style>