<template>
  <li>{{movie.title}}</li>
</template>

<script>

export default {
  name: 'movie-item',

  props: ['movie'],
  
  methods: {
      handleClick: function() {
        eventBus.$emit('send-movie', this.selectedMovie)
  },
},

}

</script>

<style scoped>
 li {
   list-style: none;
 }
</style>