<template>
  <div class="error">
    <h2 v-if="error.statusCode === 404">Page not found</h2>
    <h2 v-else>An error occurred</h2>
    <nuxt-link to="/">Go back to the home</nuxt-link>
  </div>
</template>

<script>
export default {
  props: ['error']
}
</script>


<style lang="scss" scoped>
.error {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height: 100vh;
  width: 100%;
}
</style>