<template>

    <div class="movies" >
      <movie-item :movie="movie" :genres="genres" v-for="movie in allMovies" :key="movie.id"/>
    </div>

</template>
<script>
import MovieItem from './MovieItem.vue'
export default {
    components:{
        MovieItem,
    },
    props:["allMovies", "genres"]
}
</script>
<style lang="scss" scoped>
  .movies{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-start
  }
</style>