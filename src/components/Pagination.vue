<template>
  <div class="container">
    <nav>
      <ul class="pagination justify-content-end">
        <li class="page-item" v-bind:class="{ disabled: prevPageNumber === undefined }">
          <a @click="prevPage" class="page-link" href="#">Previous</a>
        </li>
        <li class="page-item" v-bind:class="{ disabled: nextPageNumber === undefined }">
          <a @click="nextPage" class="page-link" href="#">Next</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'Pagination',
  props: ['prevPageNumber', 'nextPageNumber'],
  methods: {
    prevPage() {
      this.$emit('prev-page');
    },
    nextPage() {
      this.$emit('next-page');
    }
  }
};
</script>

<style scoped>
.page-link {
  box-shadow: none !important;
}
</style>