<template>
  <div class="movies-show">
    <div class="container">
      <h2>{{movie.title}}</h2>
      <p>Year: {{movie.year}}</p>
      <p>Director: {{movie.director}}</p>
      <p>plot: {{movie.plot}}</p>  
    </div>
    <button>
      <router-link v-bind:to="'/movies/' + movie.id + '/edit'">Edit</router-link>
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get("/api/movies/" + this.$route.params.id).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {}
};
</script>