<template>
  <div class="movies-new">
    <h1>New Movie</h1>
    <div>
      Title: <input type="text" v-model="newMovieTitle"><br>
      Year: <input type="text" v-model="newMovieYear"><br>
      Director: <input type="text" v-model="newMovieDirector"><br>
      Plot: <input type="text" v-model="newMoviePlot"><br>
      <button v-on:click="createMovie()">Add Movie</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      newMovieTitle: "",
      newMovieYear: "",
      newMovieDirector: "",
      newMoviePlot: ""
    };
  },
  created: function() {
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        director: this.newMovieDirector,
        plot: this.newMoviePlot
      };
      axios.post("/api/movies", params).then(response => {
        this.$router.push("/");
      });
    }
  }
};
</script>