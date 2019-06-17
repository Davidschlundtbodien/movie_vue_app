<template>
  <div class="movies">
    <h1>All Movies</h1>
    <div v-for="movie in movies">
      <router-link v-bind:to="'/movies/' + movie.id"><h2>{{movie.title}}</h2></router-link>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movies: [],
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      this.movies = response.data;
    });
  },
  methods: {
  }
};
</script>