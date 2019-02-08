<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <router-link to="/signup">Signup</router-link>
    <router-link to="/login">Login</router-link>
    <router-link to="/logout">Logout</router-link>


  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      results: [],
    };
  },

  created: function() {},
  methods: {
    search: function() {
      var params = {
        text: this.text
      };
      axios
        .get("/searches", params)
        .then(function(response) {
          this.results = response.data;
        }.bind(this));
    }
  },
  computed: {

  },
};
</script>
