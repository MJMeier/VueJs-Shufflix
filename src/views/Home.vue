<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <router-link to="/signup">Signup </router-link>
    <router-link to="/login">Login </router-link>
    <router-link to="/logout">Logout </router-link>

    <div>
      <h2>Search for a show:</h2>
      <p>Search: <input type="text" v-model="text" /></p>
      <button v-on:click="search()">Search show</button>
    </div>
    <div>
      <h2>Results:</h2>
      <!-- <p>{{ results }}</p> -->
      <div v-for="result in results">
        <div v-for="thing in result">
          <p>{{ thing.title }}</p>
        </div>
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
      text: "",
      id: ""
    };
  },

  created: function() {},
  methods: {
    search: function() {
      var params = {
        text: this.text
      };
      // foreach;
      axios.post("http://localhost:3000/api/searches", params).then(
        function(response) {
          // vince is a bo$$ and came up with this simple AF solution
          this.results = [];
          this.results.push(response.data.results);
        }.bind(this)
      );
      console.log("LOOK AT ME: ");
      console.log(this);
      console.log("LOOKEY DOOKEY:");
      console.log(this.results);
    }
  },
  computed: {}
};
</script>
