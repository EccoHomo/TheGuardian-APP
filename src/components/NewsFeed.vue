<template>
  <div class="container mb-3">
    <div class="card mb-2" v-bind:key="nw.id" v-for="nw in news">
        <NewsListItem v-bind:news="nw"/>
    </div>
  </div>
</template>

<script>
import NewsListItem from './NewsListItem';

export default {
  name: 'NewsFeed',
  components: {
    NewsListItem
  },
  data() {
    return {
      title: 'News'
    };
  },
  props: ['news']
};
</script>

<style scoped>
button:focus {
  box-shadow: none !important;
}
</style>