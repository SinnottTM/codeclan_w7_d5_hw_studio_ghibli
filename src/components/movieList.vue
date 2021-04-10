<template>
  <ul>
     <movie-item v-for="(movieItem, index) in movieList" :key="index" :movie="movieItem"></movie-item>
  </ul>
</template>

<script>
import movieItem from './movieItem.vue'

export default {
   name: 'movie-list',

   props: ['movieList'],

   components: {
        "movie-item": movieItem
   },
}

</script>

<style scoped>

</style>