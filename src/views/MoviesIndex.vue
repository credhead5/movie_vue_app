<template>
  <div class="movies-index">
    <h1>All Movies</h1>

    <section id="two">
      <h2>Recent Work</h2>
      <div class="row">
        <article v-for="movie in movies" class="col-6 col-12-xsmall work-item">
          <router-link :to="`/movies/${movie.id}`" class="image fit thumb">
            <img
              src="https://upload.wikimedia.org/wikipedia/en/thumb/d/db/The_Movies_Coverart.jpg/220px-The_Movies_Coverart.jpg"
              alt=""
            />
          </router-link>
          <h3>Title: {{ movie.title }}</h3>
          <p>Year: {{ movie.year }}</p>
        </article>
      </div>
    </section>
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
