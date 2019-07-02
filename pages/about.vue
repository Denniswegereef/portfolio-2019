<template>
  <main class="about">
    <div class="about__content">
      <h1>About myself</h1>
      <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."</p>
    </div>
    <img class="about__image" src="~/static/images/myself.png" alt />
  </main>
</template>

<script>
export default {
  layout: 'About'
}
</script>

<style lang="scss" scoped>
.about {
  max-width: 60rem;
  margin: 0 auto;
  position: relative;
  margin-top: 10rem;
  padding: 0 2rem;

  &__content {
    z-index: 9;
  }
  &__image {
    z-index: -1;
    max-width: 20rem;
    position: fixed;
    top: 20vh;
    right: 20vh;
  }
}
</style>
