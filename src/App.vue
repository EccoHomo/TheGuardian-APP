<template>
  <div id="app">
    <Header/>
    <SearchForm v-on:search="search"/>
    <NewsFeed v-if="ShowFeed" v-bind:news="news"/>
    <SearchResults
      v-if="news.length > 0 && ShowResults"
      v-bind:news="news"
      v-bind:reformattedSearchString="reformattedSearchString"
    />
    <Pagination
      v-if="news.length > 0"
      v-bind:prevPageNumber="api.prevPageNumber"
      v-bind:nextPageNumber="api.nextPageNumber"
      v-on:prev-page="prevPage"
      v-on:next-page="nextPage"
    /> 
  </div>
</template>

<script>
import Header from './components/layout/Header';
import SearchForm from './components/SearchForm';
import NewsFeed from './components/NewsFeed';
import SearchResults from './components/SearchResults';
import Pagination from './components/Pagination';
import axios from 'axios';


export default {
  name: 'app',
  components: { Header, SearchForm, NewsFeed, SearchResults, Pagination},
  data(){
    return{
      news: [],
      ShowFeed: true,
      ShowResults: true,
      reformattedSearchString: '',
      api: {
        baseUrl: 'https://content.guardianapis.com/search?',
        q: '',
        key: 'd5f41dcd-c51f-4a67-8610-8c18a57e7ecd',
        currentPage: '',
        nextPageNumber: '',
        prevPageNumber: '',
      }
    };
  },
  methods: {
    search(searchParams){
      this.ShowFeed = false;
      this.ShowResults = true;
      this.reformattedSearchString = searchParams.join(' ');
      this.api.q = searchParams.join('+');
      const { baseUrl, q, key} = this.api;
      const apiUrl = `${baseUrl}&q=${q}&api-key=${key}`;
      this.getData(apiUrl);
    },

    prevPage(){
      const { baseUrl, prevPageNumber, q, key} = this.api;
      const apiUrl = `${baseUrl}page=${prevPageNumber}&q=${q}&api-key=${key}`;
      this.getData(apiUrl);
    },

    nextPage(){
      const { baseUrl, nextPageNumber, q, key} = this.api;
      const apiUrl = `${baseUrl}page=${nextPageNumber}&q=${q}&api-key=${key}`;
      this.getData(apiUrl);
    },

    getData(apiUrl){
      axios.get(apiUrl)
        .then(res => {
          this.news = res.data.response.results;
          this.api.prevPageNumber = (res.data.response.currentPage) !== 1 ? ((res.data.response.currentPage) -1) : (res.data.response.currentPage);
          this.api.nextPageNumber = (res.data.response.currentPage) + 1;
        })
        .catch(error => console.log(error));
    }
  },
  created(){
    this.ShowFeed = true;
    this.ShowResults = false;
    const { baseUrl, key} = this.api;
    const apiUrl = `${baseUrl}&api-key=${key}`;
    this.getData(apiUrl);
  }
}
</script>

<style>
</style>
