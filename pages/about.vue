<template>
  <section class="about">
    <h2 class="about__title">Some straight facts about me</h2>

    <div class="about__image"></div>

    <p class="about__content">Here comes the content of me what i'm wanna tell</p>
  </section>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.about {
  display: grid;
  &__title {
  }
  &__image {
    height: 400px;
    width: 250px;
    background-color: red;
  }
  &__content {
  }
}
</style>
