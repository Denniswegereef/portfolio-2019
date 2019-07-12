<template>
  <main class="about">
    <img ref="image" class="about__image" src="~/static/images/myself.png" alt />

    <div class="about__content" ref="content">
      <Header>
        <h2>About me</h2>
      </Header>
      <p>My name is Dennis Wegereef 23-year-old dutch guy, and I am currently living in Amsterdam. I'm a student at the University of Applied Sciences Amsterdam, studying Communication Multimedia Design. I finished my third year and moving up to my graduation year. The study is focused on concepts, user experience, and creating digital products while keeping the end-user in mind.</p>
      <p>So a little about me I'm an avid sneaker collector trying to get the most exclusive Nike Air Max 1s. My passion doesn't stop there, with two friends. We have a webshop called Outsole.nl where we sell more collectible sneakers all around the world, where we are the market leader in selling collectible Nike Air Max 1s. With more than 300.000 unique visitors in 2018. Where I mostly helped to create the webshop and content for all the social channels.</p>
      <p>At the moment I've just finished the minor Web Development, also at the University of Applied Sciences. During this minor, we have been working with multiple and varying front-end aspects. The minor for the past half-year covers many topics like accessibility on the web, real-time connections, performance, progressive enhancement, web servers with Express, and a-lot of CSS and 'vanilla' JavaScript.</p>
      <p>In my graduation year, I have to do an internship for 20 weeks starting from the 1st of September 2019 till the 1st of February 2020. Therefore I'm looking for a front-end internship focused on enhancing the web and building excellent products. And would like to talk more about the possibilities and my learning goals towards the internship.</p>
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
