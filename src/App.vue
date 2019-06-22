<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/movies">Movies</router-link>|
      <router-link to="/movies/new">New Movie</router-link>|
      <span v-if="isLoggedIn()">
        <router-link to="/logout">Logout</router-link>
      </span>
      <span v-else>
        <router-link to="/signup">Signup</router-link>
        <router-link to="/login">Login</router-link>
      </span>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
    };
  },
  created: function() {},
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem('jwt');
    }
  }
};
</script>
