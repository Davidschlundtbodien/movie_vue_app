
<template>
  <div class="movies-edit">
    
    <h1>Edit movie</h1>

    <form v-on:submit.prevent="submit()">
      <div class="container">
        Title: <input type="text" v-model="movie.title"><br>
        Director: <input type="text" v-model="movie.director"><br>
        Year: <input type="number" v-model="movie.year"><br>
        Plot: <input type="text" v-model="movie.plot">
      </div>
      <button type="submit">Update</button>
      <button>Delete</button>
    </form>

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
  methods: {
    submit: function() {
      var params = {
        title: this.movie.title,
        director: this.movie.director,
        year: this.movie.year,
        plot: this.movie.plot
      };
      axios.patch("/api/movies/" + this.movie.id, params).then(response => {
        this.$router.push("/movies/" + this.movie.id);
      });
    },
    destroyMovie: function(movie) {
      axios.delete("/api/movie/" + movie.id).then(response => {
        this.$router.push("/");
      });
    }
  }
};
</script>