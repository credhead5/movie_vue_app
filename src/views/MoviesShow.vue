<template>
  <div class="movies-show">
    <div class="text-center">
      <h1>{{ movie.title }}</h1>
    </div>
    <div v-for="movie in movies" v-on:click="currentMovie = movie" v-bind:class="{ selected: movie === currentMovie }">
      <h4>Director</h4>
      <p>{{ movie.director }}</p>
    </div>

    movies user id: {{ movie.user.id }}
    <br />
    current user id: {{ $parent.getUserId() }}
    <br />

    <router-link class="btn btn-warning" v-if="movie.user.id == $parent.getUserId()" :to="`/movies/${movie.id}/edit`">
      Edit
    </router-link>
  </div>
</template>

<style>
.selected {
  color: white;
  background-color: steelBlue;
  transition: background-color 1s ease;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {}
};
</script>
