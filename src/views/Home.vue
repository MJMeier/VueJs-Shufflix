<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <router-link to="/signup">Signup</router-link>
    <router-link to="/login">Login</router-link>
    <router-link to="/logout">Logout</router-link>

    <div>
      <h2>Search for a show:</h2>
      <p>Search: <input type="text" v-model="text" /></p>
      <button v-on:click="search()">Search show</button>
    </div>
    <div>
      <h2>Results:</h2>
      <div v-for="result in results">
        <p>Title: {{ result.title }}</p>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Welcome to our app Shufflix!",
      results: [],
      text: ""
    };
  },

  created: function() {},
  methods: {
    search: function() {
      var params = {
        text: this.text
      };
      axios.post("http://localhost:3000/api/searches", params).then(
        function(response) {
          // console.log(" response is: ", response);
          this.results.push(response.data.results);
        }.bind(this)
      );
      console.log("LOOK AT ME: ");
      console.log(this);
    }
  },
  computed: {}
};
</script>
