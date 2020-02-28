<template>
  <div class="movies-index">
    <h1>All Movies</h1>
    <div v-for="movie in movies">
      <h1>{{ movie.title }}</h1>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movies: []
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
      console.log(this.movies);
    });
  },
  methods: {}
};
</script>
