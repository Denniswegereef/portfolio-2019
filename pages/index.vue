<template>
  <div>
    <!-- <Splash/> -->

    <main class="work-container">
      <nuxt-link
        v-for="(item, index) in $options.workData"
        v-bind:key="index"
        :to="'work/' + item.id"
      >
        <workItem
          :title="item.title"
          :image="item.image"
          :description="item.description"
          :index="index"
        />
      </nuxt-link>
    </main>
  </div>
</template>

<script>
import workData from '~/static/work.json'
import workItem from '~/components/work/item.vue'

import Splash from '~/components/Splash.vue'

export default {
  workData,
  components: {
    workItem,
    Splash
  }
}
</script>

<style lang="scss" styled>
.work-container {
  background-color: #1c1c1c;
  width: 100%;
  padding: 20rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 80rem;
}
</style>
