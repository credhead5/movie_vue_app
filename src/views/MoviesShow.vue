<template>
  <div class="movies-show">
    <div class="text-center">
      <h1>{{ movie.title }}</h1>
    </div>
    <div v-for="movie in movies">
      <h4>Director</h4>
      <p>{{ movie.director }}</p>
    </div>
    <router-link class="btn btn-warning" v-if="movie.user.id == $parent.getUserId()" :to="`/movies/${movie.id}/edit`">
      Edit
    </router-link>
  </div>
</template>

<style></style>

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
