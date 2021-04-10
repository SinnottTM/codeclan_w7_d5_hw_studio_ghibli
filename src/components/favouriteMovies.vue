<template>
  <ul>
        <li v-for="(movie, id) in favouriteMovies" :key="id" :movie="movie">
          <button @click="removeMovie(movie), handleRemoveClick">Remove Movie</button>
          {{movie.title}}
        </li>
  </ul>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'favourite-movies', 
    data(){
    return {
      newFavouriteMoviesList: [],
    }
  },

    props: [
        'favouriteMovies',
        // 'removeMovie'
        // 'eventBusOn'
    ],

    methods: {
      removeBeer: function(movieRemoval){
        this.newFavouriteMoviesList = this.favouriteMovies.filter(movie => movie.title !== movieRemoval.title)
        console.log(this.favouriteMovies);
        console.log(this.newFavouriteMoviesList);
        eventBus.$emit('new-favourite-movie-list', this.newFavouriteMoviesList)
      },
               
    },
}

</script>

<style scoped>
 li {
   list-style: none;
 }
</style>