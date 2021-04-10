<template>
  <div id="app">
     <h1>Studio Ghibli Film App</h1>
      <div class="main-container">

        <br><br>

        <!-- Movie drop down list -->
        <label for="movie_select">Select a Movie:</label>
        <select id="movie_select" v-model="selectedMovie">
          <option disabled value="">Select a movie</option>
          <option v-for="movie in movieList" :key="movie" :value="movie">{{movie.title}}</option>
        </select>

        <br><br>

        <!-- Movie details info -->
        <movie-details :movie="selectedMovie" v-if="selectedMovie"></movie-details>

        <!-- Add to Favourites -->
        <button @click="addToFavourites">Add to favourites</button>
        <favourite-movies :favouriteMovies="favouriteMoviesList"></favourite-movies>

      </div>
  </div>
</template>

<script>

import {eventBus} from './main.js';

import movieList from './components/movieList.vue';
import movieDetails from './components/movieDetails.vue';
import favouriteMovies from './components/favouriteMovies.vue'


export default {
  name: 'App',

  components: {
    "movie-list": movieList,
    "movie-details": movieDetails,
    'favourite-movies': favouriteMovies,
  },

  data(){
    return {
      movieList: [],
      selectedMovie: null,
      searchedMovie: null,
      favouriteMoviesList: [],
    }
  },
  
  methods: {
    addToFavourites: function(){
      if (!this.favouriteMoviesList.includes(this.selectedMovie)) {
        this.favouriteMoviesList.push(this.selectedMovie)
      }
      // console.log(this.favouriteMoviesList)
   },

  //   handleRemoveClick: function(){ eventBus.$on('new-favourite-movie-list', (newFavouriteMovieList) => {
  //     // console.log("event triggered")
  //     this.favouriteMovieList = newFavouriteMovieList;
  //   })
   
  //  }
  },

  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(movieList => this.movieList = movieList)
    console.log(movieList)

    eventBus.$on('send-movie', (movie) => {
    // console.log("event triggered", movie)
    this.selectedMovie = movie;
    })

    eventBus.$on('movie-removed', (movie) => {
    this.selectedMovie = movie;
    this.favouriteMoviesList.remove(this.selectedMovie)
  })
 },

}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.main-container {
  /* display: grid;
  align-self: center; */
  /* justify-content: space-between;
  margin: auto; */
}

</style>
