<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div class="st-tabs">
    <span class="st-single-tab top-rated" :class="{'active' : activePage == 'topRated'}" @click="getTopRatedMovies()">Top-rated Movies <span v-show="totalResultsTopRated>0">({{totalResultsTopRated}})</span></span>
    <span class="st-single-tab upcoming" :class="{'active' : activePage == 'upcoming'}" @click="getUpcomingMovies()">Upcoming <span v-show="totalResultsUpcoming>0">({{totalResultsUpcoming}})</span></span>
  </div>
  <DefaultTemplate :results="results" :page="page" :totalPages="totalPages" @getMoreResults="getMoreResults"></DefaultTemplate>
</template>

<script>

import axios from 'axios';
import DefaultTemplate from "./components/DefaultTemplate.vue";

export default {
  name: 'App',
  components: {DefaultTemplate},
  data() {
    return {
      results: [],
      page : 1,
      totalPages : 1,
      totalResultsTopRated : 0,
      totalResultsUpcoming : 0,
      activePage : 'topRated'
    }
  },

  mounted(){
    this.getTopRatedMovies();
  },

  methods: {
    getTopRatedMovies() {
      if(this.activePage === 'upcoming') {
        this.reset();
      }
      this.activePage = 'topRated';
     axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=63ea4c3db3b7814af9bde6ae59b01aa7&page=${this.page}`)
         .then(response => {
           this.totalPages = response.data.total_pages;
           this.totalResultsTopRated = response.data.total_results;
           if(this.page === 1)
           this.results = response.data.results;
           else if(this.page > 1){
             this.results = this.results.concat(response.data.results)
           }
         }).catch(error => {
           console.log(error);
     })
    },

    getUpcomingMovies(){
      if(this.activePage === 'topRated') {
        this.reset();
      }
      this.activePage = 'upcoming';
      axios.get(`https://api.themoviedb.org/3/movie/upcoming?api_key=63ea4c3db3b7814af9bde6ae59b01aa7&page=${this.page}`)
          .then(response => {
            this.totalPages = response.data.total_pages;
            this.totalResultsUpcoming = response.data.total_results;
            if(this.page === 1)
              this.results = response.data.results;
            else if(this.page > 1){
              this.results = this.results.concat(response.data.results)
            }
          }).catch(error => {
        console.log(error);
      })
    },

    reset(){
          this.results = [];
          this.page = 1;
          this.totalPages = 1;
          this.totalResultsTopRated = 0;
          this.totalResultsUpcoming = 0;
    },

    getMoreResults(){
      this.page = this.page + 1;
      if(this.page <= this.totalPages){
       if(this.activePage === 'topRated')
        this.getTopRatedMovies();
       else
         this.getUpcomingMovies();
      }
    }
  }
}

</script>

<style>
#app{
  text-align: center;
}

.st-tabs {
  width: 50%;
  display: flex;
  margin: 0 auto !important;
  justify-content: center;
  padding-bottom: 20px;
}

span.st-single-tab {
  width: 50%;
  border: 1px solid #f1f1f1;
  text-align: center;
  padding: 9px;
  cursor: pointer;
}

span.st-single-tab.top-rated {
  background: #BEEFEC;
}

span.st-single-tab.top-rated.active {
  border-color: #7ed4e9;
}

span.st-single-tab.upcoming {
  background: #FFD6CE;
}

span.st-single-tab.upcoming.active {
  border-color: #f6a2b0;
}
</style>
