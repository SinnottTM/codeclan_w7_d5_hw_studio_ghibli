<template>
  <section>
    <br>
    <!-- <img :src="movie.image_url" alt="Movie image" style="height:200px"> -->
    <h3>Name: {{movie.title}}</h3>
    <p>Original Title: {{movie.original_title_romanised}}</p>
    <!-- <p>Plot: {{movie.description}}</p> -->
    <p>Director: {{movie.director}}</p>
    <!-- <p>Producer: {{movie.producer}}</p> -->
    <p>Release Date: {{movie.release_date}}</p>
    <p>Running Time: {{movie.running_time}}</p>
    <p>Rotten Tomatoes Score: {{movie.rt_score}}</p>
    
  </section>

</template>

<script>
export default {
    name: 'movie-details',
    props: ['movie']
}
</script>

<style scoped>

</style>