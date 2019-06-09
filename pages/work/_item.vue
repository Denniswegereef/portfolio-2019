<template>
  <div>
    <h1>{{item.title}}</h1>
  </div>
</template>

<script>
import workData from '~/static/work.json'

export default {
  workData,
  head() {
    return {
      title: this.item.title
    }
  },
  data() {
    return {
      id: this.$route.params.item
    }
  },
  validate({ params }) {
    if (workData.find(item => item.id === params.item)) {
      return true
    }
  },
  computed: {
    item() {
      return workData.find(item => item.id === this.id)
    }
  }
}
</script>

<style lang="scss" scoped>
</style>