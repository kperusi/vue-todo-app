<template>
  <h1>Movie List Details</h1>
  <div class="wrapper">
    <div class="main" v-for="(movie, index) in movies" :key="index">
      <h1>Title:{{ movie.movieName }}</h1>
      <h3>Rating:{{ movie.rating }}</h3>
      <h3>Duration:{{ movie.duration }} hr</h3>
      <button @click="$emit('removeMovie', movie.movieId,movie.movieName)">Remove Movie from list</button>
    </div>
  

  </div>
  <!-- <button @click="$emit('removeMovie')">Remove the last added movie</button> -->
</template>

<script>

export default {
  props: {
    title: String,
    rate: String,
    movies:Array,
  },
  data() {
    return {};
  },
  methods:{
    
  },
  emits:['removeMovie'],
 
};
</script>
<style scoped>
.main {
  border: 2px solid rgb(176, 176, 176);
  border-radius: 10px;
  width: 200px;
  margin: 0 auto;
  margin-bottom: 10px;
 
}
.wrapper {
  border: solid;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
