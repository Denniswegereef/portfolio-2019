<template>
  <div>
    <section class="splash">
      <splashTitle/>
    </section>

    <main class="work-container">
      <div v-for="(item, index) in $options.workData" v-bind:key="index">
        <workItem
          :title="item.title"
          :image="item.image"
          :description="item.description"
          :index="index"
        />
      </div>
    </main>
  </div>
</template>

<script>
import workData from '~/static/work.json'
import workItem from '~/components/work/item.vue'

import splashTitle from '~/components/splash/title.vue'

export default {
  workData,
  components: {
    workItem,
    splashTitle
  }
}
</script>

<style lang="scss" styled>
.splash {
  height: 100vh;
  width: 100%;
  background-color: #1c1c1c;
}

.work-container {
  background-color: #1c1c1c;
  width: 100%;
  padding: 20rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 80rem;
}
h2 {
  color: blue;
}
</style>
