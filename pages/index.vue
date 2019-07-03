<template>
  <div>
    <Splash />

    <main class="work-container">
      <article v-for="(item, index) in $options.workData" v-bind:key="index">
        <workItem
          :title="item.title"
          :image="item.image"
          :description="item.description"
          :index="index"
          :id="item.id"
        />
      </article>
    </main>

    <Footer />
  </div>
</template>

<script>
import workData from '~/static/work.json'

import Splash from '~/components/Splash.vue'
import workItem from '~/components/work/item.vue'
import Footer from '~/components/Footer.vue'

export default {
  workData,
  components: {
    workItem,
    Splash,
    Footer
  },
  layout: 'Default'
}
</script>

<style lang="scss" styled>
@import '~assets/css/config';

.work-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: baseline;
  transform: translateY(-10vh);
  padding: 0 2rem;

  @media screen and (min-width: 40rem) {
    max-width: 70rem;
    margin: 0 auto;
  }

  article {
    &:nth-child(odd) {
      @media screen and (min-width: 40rem) {
        align-self: flex-end;
      }
    }
    &:nth-child(even) {
      @media screen and (min-width: 40rem) {
        align-self: flex-start;
      }
    }
  }
}
</style>
