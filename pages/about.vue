<template>
  <main class="about">
    <img ref="image" class="about__image" src="~/static/images/myself.png" alt />

    <div class="about__content" ref="content">
      <Header>
        <h2>About me</h2>
      </Header>
      <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."</p>
    </div>

    <div class="about__socials" ref="socials">
      <p>here comes the socials</p>
    </div>
  </main>
</template>

<script>
import Header from '~/components/header.vue'

export default {
  components: {
    Header
  },
  mounted() {
    this.showItem()
  },
  methods: {
    showItem() {
      TweenMax.from(this.$refs.content, 0.8, {
        delay: 0.5,
        opacity: 0,
        y: 20
      })

      TweenMax.from(this.$refs.socials, 0.8, {
        delay: 1.3,
        opacity: 0,
        y: 20
      })

      TweenMax.from(this.$refs.image, 0.5, {
        delay: 0.9,
        opacity: 0,
        x: -20
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.about {
  max-width: 60rem;
  margin: 0 auto;
  position: relative;
  margin-top: 10rem;
  padding: 0 2rem;
  display: grid;
  grid-template-areas:
    'image'
    'content'
    'socials';
  grid-row-gap: 2em;
  grid-column-gap: 2em;

  @media screen and (min-width: 40rem) {
    margin-top: 10rem;
    grid-column-gap: 4em;
    grid-template-areas:
      'image content content '
      'image content content '
      'socials socials socials ';
  }

  &__content {
    grid-area: content;
    z-index: 9;
  }

  &__image {
    width: 100%;
    grid-area: image;
    margin-right: 2rem;
  }

  &__socials {
    grid-area: socials;
    display: flex;
    align-self: center;
    justify-content: center;
  }
}
</style>
