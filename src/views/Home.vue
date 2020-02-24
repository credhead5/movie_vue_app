<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <h1>New Movie</h1>

    <div>
      Title:
      <input type="text" v-model="newMovieTitle" />
      <br />
      Year:
      <input type="text" v-model="newMovieYear" />
      <br />
      Plot:
      <input type="text" v-model="newMoviePlot" />
      <br />
      Director:
      <input type="text" v-model="newMovieDirector" />
      <br />
      English:
      <input type="text" v-model="newMovieEnglish" />
      <br />

      <button v-on:click="createMovie()">Create Contact</button>
    </div>

    <div>
      <div v-for="movie in movies">
        <h2>{{ movie.title }}</h2>

        <button v-on:click="movie.showExtraInfo = !movie.showExtraInfo">More Info</button>
        <div v-if="movie.showExtraInfo">
          <p>Title: {{ movie.title }}</p>
          <p>Year: {{ movie.year }}</p>
          <p>Plot: {{ movie.plot }}</p>
          <p>Director: {{ movie.director }}</p>
          <p>English: {{ movie.english }}</p>
          <div>
            <!-- edit -->
            {{ movie }}
            <h3>Edit Movie</h3>
            Title:
            <input type="text" v-model="movie.title" />
            <br />
            Year:
            <input type="text" v-model="movie.year" />
            <br />
            Plot:
            <input type="text" v-model="movie.plot" />
            <br />
            Director:
            <input type="text" v-model="movie.director" />
            <br />
            English:
            <input type="text" v-model="movie.english" />
            <br />
            <button v-on:click="updateMovie(movie)">Update</button>
            <br />
            <button v-on:click="destroyMovie(movie)">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: null
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      response.data.forEach(movie => {
        movie.showExtraInfo = false;
      });
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          this.movies.push(response.data);
          this.newMovieTitle = "";
          this.newMovieYear = "";
          this.newMoviePlot = "";
          this.newMovieDirector = "";
          this.newMovieEnglish = "";
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
        english: movie.english
      };
      axios
        .patch("/api/movies/" + movie.id)
        .then(response => {
          console.log("Success", response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
    destroyMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("Success", response.data);
        // find index of movie object in movies array
        var index = this.movies.indexOf(movie);
        //remove that index from movies array
        this.movies.splice(index, 1);
      });
    }
  }
};
</script>
