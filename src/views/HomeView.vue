<template>
  <div class="home container">

    <movies-header @searchMovieByDate="searchMovieByDate"/>

    <movies :allMovies="allMovies" :genres="genres"/>

    <pagination 
      v-if="!filteredFlag"
      :itemsCount="movies.length"
      :pageSize="pageSize" 
      :currentPage="currentPage"
      @onPageChange="onPageChange" />

     <p v-if="!filteredFlag" class="results">Showing results {{startIndex+1}} - {{pageSize*(currentPage)}}</p>
  </div>
</template>

<script>

import axios from 'axios'
import Movies from '../components/movies/MoviesWrapper.vue'
import _ from 'lodash';
import Pagination from '../components/shared/Pagination.vue'
import MoviesHeader from '../components/movies/MoviesHeader.vue';
export default {
  
  name: 'HomeView',
  components: {
    Movies,
    Pagination,
    MoviesHeader,
  },
  data: () =>({
    movies:[],
    genres:[],
    currentPage:1,
    pageSize:10,
    allMovies:[],
    startIndex:1,
    filteredFlag:false,
  }),
  created(){
    this.getListOfMovies()
    this.getGenres()
  },
  watch:{
    currentPage(){
      this.allMovies = this.paginate(this.movies, this.currentPage, this.pageSize)
    }
  },
  methods:{
    getListOfMovies(){
      axios.get(`https://api.themoviedb.org/3/discover/movie?api_key=f62f750b70a8ef11dad44670cfb6aa57&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1&with_watch_monetization_types=flatrate`)
      .then((response) =>{
        this.movies = response.data.results
        this.allMovies = this.paginate(this.movies, this.currentPage, this.pageSize)
        })
    },
    getGenres(){
      axios.get('https://api.themoviedb.org/3/genre/movie/list?api_key=f62f750b70a8ef11dad44670cfb6aa57&language=en-US')
      .then((response) =>{
        this.genres = response.data.genres
      })
    },
    paginate(items, pageNumber, pageSize){
      this.startIndex = (pageNumber - 1) * pageSize;
      return _(items)
          .slice(this.startIndex)
          .take(pageSize)
          .value()
    },
    onPageChange(page){
      this.currentPage = page
    },
    searchMovieByDate(dateValue){
      this.filteredFlag=true
      const movies = this.movies
      const filteredMovies = movies.filter(movie => movie.release_date === dateValue)
      this.allMovies = filteredMovies
    }
  }
}
</script>
<style lang="scss" scoped>


  .results{
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    color: #989898;
    margin-top:14px;
  }
</style>
