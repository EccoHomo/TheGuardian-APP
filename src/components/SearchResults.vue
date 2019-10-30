<template>
  <div class="container mb-3">
    <div class="d-flex mb-3">
      <div class="mr-auto">
        <h3>Search Results for "{{ reformattedSearchString }}"</h3>
      </div>
    </div>
    <div class="card mb-2" v-bind:key="nw.id" v-for="nw in news">
        <NewsListItem v-bind:news="nw"/>
    </div>
  </div>
</template>

<script>
import NewsListItem from './NewsListItem';

export default {
  name: 'SearchResults',
  components: {
    NewsListItem
  },
  data() {
    return {
      title: 'Search Results'
    };
  },
  props: ['news', 'reformattedSearchString']
};
</script>

<style scoped>
button:focus {
  box-shadow: none !important;
}
</style>