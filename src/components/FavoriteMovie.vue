<template>
  <h1>{{ name }}</h1>
  <div class="form-wrap">
    <form action="" class="form">
      <label for="movieName">Enter Movie Name</label>
      <input type="text" class="inputs" v-model="movieName" />
      <label for="rating">Enter Movie Rating</label>
      <input type="text" class="inputs" v-model="movieRate" />
      <label for="movieTime">Enter Movie Duration</label>
      <input type="text" class="inputs" v-model="movieTime" />
      <button class="btn" type="button" @click="addHandler">Add</button>
      
    </form>
  </div>

  <MovieList :movies="movies" @removeMovie="removeMovie" />
  <div>Data fetch
  <div v-if="loading" :style="{height:'50px'}">Data loading</div>
  <div v-for="(eachData,index) in userData" :key="index">{{ eachData.title }}</div>
  </div>
</template>

<script>
// import { json } from "body-parser";
import MovieList from "./MovieList.vue";
export default {
  data() {
    return {
      name: "My Favorite Movie List",
      movieName: "",
      movieRate: "",
      movieTime: "",
      movies: [
        {
          movieId: 1,
          movieName: "Merlin",
          rating: "12",
          duration: "2",
        },
      ],
      userData: [],
      error: "",
      loading: true,
    };
  },

  methods: {
    addHandler() {
      console.log(this.userData);
      this.movies.push({
        movieId: this.movies.length + 1,
        movieName: this.movieName,
        rating: this.movieRate,
        duration: this.formatedDuration,
      }),
        // console.log(this.movies)
        (this.movieName = "");
      this.movieRate = "";
      this.movieTime = "";
    },

    removeMovie(id) {
      this.movies = this.movies.filter(function (movie) {
        console.log("this movieId", movie.movieId);
        return movie.movieId !== id;
      });
    },
    users() {
      fetch("https://jsonplaceholder.typicode.com/posts")
        .then((data) => {
          return data.json();
        })
        .then((data) => {
          this.userData = data;
          // console.log(data)
        })
        .catch((error) => {
          this.error = error;
        })
        .finally(() => {
          this.loading = false;
        });
    },
  },
  computed: {
    formatedDuration() {
      if (this.movieTime > 60) {
       
        return this.movieTime / 60;
      } else return this.movieTime;
    },
  },

  components: {
    MovieList,
  },
  mounted() {
    this.users();
  },

  watch: {
    movies: {
      deep: true,
      handler() {
        // console.log(newValue)
        // console.log(`new movie add ${newValue} is add`)
      },
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
  border: 2.3px solid rgb(176, 174, 174);
  width: 40%;
  border-radius: 10px;
  gap: 10px;
  padding: 10px;
}
.form-wrap {
}
.inputs {
  width: 280px;
  height: 30px;
}
.btn {
  height: 60px;
  width: 190px;
  border-radius: 8px;
  outline: none;
  border: 2px solid rgb(203, 203, 203);
  font-weight: 700;
  color: gray;
  background-color: black;
}
</style>
