<template>
  <div class="movies-new">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Movie</h1>
        <img v-if="status" v-bind:src="`https://http.cat/${status}`" />
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>Title:</label>
          <input type="text" class="form-control" v-model="title" />
        </div>
        <div class="form-group">
          <label>Year:</label>
          <input type="text" class="form-control" v-model="year" />
        </div>
        <div class="form-group">
          <label>Plot:</label>
          <input type="text" class="form-control" v-model="plot" />
          <small v-if="plot" v-bind:class="{ 'text-danger': 30 - plot.length < 5 }">
            {{ 30 - plot.length }} characters remaining
          </small>
        </div>
        <div class="form-group">
          <label>Director:</label>
          <input type="text" class="form-control" v-model="director" />
        </div>
        <input type="submit" class="btn btn-primary" value="Create New" />
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      year: "",
      plot: "",
      director: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
        director: this.director
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          this.$router.push("/movies");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>
