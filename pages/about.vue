<template>
  <main class="about">
    <img
      ref="image"
      class="about__image"
      src="~/static/images/pictureofme.jpg"
      alt="Dennis Wegereef"
    />

    <div class="about__content" ref="content">
      <h2>About Dennis</h2>
      <p>My name is Dennis Wegereef 23-year-old dutch guy, and I am currently living in Amsterdam. I'm a student at the University of Applied Sciences Amsterdam, studying Communication Multimedia Design. I finished my third year and moving up to my graduation year. The study is focusing on concepts, user experience, and creating digital products while keeping the end-user in mind.</p>
      <p>So a little about me I'm an avid sneaker collector trying to get the most exclusive Nike Air Max 1s. My passion doesn't stop there, with two friends. We have a webshop called Outsole.nl, where we sell more collectible sneakers all around the world. We are the market leader in selling collectible Nike Air Max 1, with more than 300.000 unique visitors in 2018. I mostly helped to create and build the webshop in Wordpress in combination with Woocommerce. Also, I helped to produce content for their social channels, including graphic work and photography.</p>
      <p>At the moment I've just finished the minor Web Development at the University of Applied Sciences. During this minor, we have been working with multiple and varying front-end aspects. The minor for the past half-year covers many topics like accessibility on the web, real-time connections, performance, progressive enhancement, web servers with Express, and a-lot of CSS and 'vanilla' JavaScript.</p>
      <p>My experience on the web exists out of multiple aspects ranging from front-end to back-end languages. I know HTML5, CSS, and native Javascript. But more specific, I have experience with frameworks such as Vue.JS and React and also with libraries like D3 and GSAP. Besides these languages I have an excellent understanding of Node.JS as an extension on building server-side products with Express. I use preprocessor scripting languages such as Sass and Less on daily basis, and build automatisation systems with Gulp and Webpack.</p>
      <p>In my graduation year, I have to do an internship for 20 weeks starting from the 1st of September 2019 till the 1st of February 2020. Therefore I'm looking for a front-end internship focused on enhancing the web and building excellent products. And I would like to talk more about the possibilities and my learning goals towards the internship.</p><
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
      TweenMax.staggerFrom(
        this.$refs.content.children,
        0.8,
        {
          delay: 0.5,
          opacity: 0,
          y: 20
        },
        0.2
      )

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
  h2 {
    margin-bottom: 2rem;
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
