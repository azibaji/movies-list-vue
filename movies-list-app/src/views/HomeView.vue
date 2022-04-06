<template>
  <div class="home container">
    
    <div class="header">
      <div>
        <label>Search by release date:</label>
        <input type="date" value="2018-07-22" id="movie-date"/>
      </div>
      
      <button @click="searchMovieByDate"> search</button>
    </div>

    <div class="movies" >
      <movie-item :movie="movie" :genres="genres" v-for="movie in allMovies" :key="movie.id"/>
    </div>

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
import MovieItem from '../components/movies/MovieItem.vue'
import _ from 'lodash';
import Pagination from '../components/shared/Pagination.vue'
export default {
  
  name: 'HomeView',
  components: {
    MovieItem,
    Pagination
  },
  data: () =>({
    movies:[],
    genres:[],
    currentPage:1,
    pageSize:10,
    allMovies:[],
    startIndex:1,
    filteredFlag:false
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
    searchMovieByDate(){
      this.filteredFlag=true
      const movies = this.movies
      const datechosen = document.getElementById('movie-date').value
      const filteredMovies = movies.filter(movie => movie.release_date === datechosen)
      this.allMovies = filteredMovies
    }
  }
}
</script>
<style lang="scss" scoped>
  .header{
      background: #E2E2E2;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      padding: 18px 80px;
      margin-bottom: 78px;
      align-items: center;
      label{
        margin-right:24px;
        font-weight: 400;
        font-size: 16px;
        line-height: 19px;
      }
      input{
        border: 1px solid #CFCFCF
      }
      button{
         background: #549DF2;
         border-radius: 100px;
         color: white;
         align-self: center;
         padding: 7px 14px;
         text-decoration: none;
         border:0px;
      }
  }
  .movies{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-start
  }
  .results{
    font-weight: 400;
    font-size: 16px;
    line-height: 19px;
    color: #989898;
    margin-top:14px;
  }
</style>
