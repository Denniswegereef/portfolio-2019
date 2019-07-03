<template>
  <div class="work">
    <header class="work__header">
      <h1>{{ item.title }}</h1>
    </header>

    <div class="work__meta">
      <ul>
        <li>
          <span>Date</span>
          {{ item.date }}
        </li>
        <li>
          <span>Client</span>
          {{ item.client }}
        </li>
        <li>
          <span>Role</span>
          {{ item.role }}
        </li>
        <li>
          <a :href="item.link">
            <span>Online link</span>
          </a>
        </li>
        <li>
          <a :href="item.github">
            <span>Repository</span>
          </a>
        </li>
      </ul>
    </div>

    <div class="work__content">
      <p>{{ item.description }}</p>
    </div>

    <footer class="work__footer">
      <nuxt-link to="/">Go back</nuxt-link>
    </footer>
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
  },
  layout: 'Default'
}
</script>

<style lang="scss" scoped>
@import '~assets/css/config';

.work {
  max-width: 60rem;
  margin: 0 auto;
  margin-top: 5rem;
  display: grid;
  grid-template-areas:
    'header'
    'meta'
    'content'
    'footer';
  padding: 0 2rem;
  grid-row-gap: 3em;

  @media screen and (min-width: 40rem) {
    padding: 0;
    grid-template-areas:
      'header header header '
      'meta content content'
      'footer footer footer';
    grid-column-gap: 5em;
    grid-row-gap: 5em;
  }

  &__header {
    grid-area: header;
    width: 100%;
    height: 200px;
    background-color: red;
  }

  &__meta {
    color: $color-white;
    grid-area: meta;
    ul {
      padding: 0;
      list-style-type: none;
    }

    span {
      font-weight: bold;
    }
  }

  &__footer {
    grid-area: footer;
    width: 100%;
    height: 200px;
    background-color: blue;
  }
}
</style>