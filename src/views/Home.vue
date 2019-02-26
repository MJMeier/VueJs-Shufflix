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
      <!-- <p>{{ results }}</p> -->
      <div v-for="result in results">
      <h2>Results:</h2>
        <div v-for="thing in result">
          <p>{{ thing.title }}</p>
          <img v-bind:src="thing.pic" />
          <button v-model="id" v-on:click="shuffleSeason(thing)">
            Shuffle season
          </button>
          <div v-if="thing.visible">
            <h3>You should watch episode:</h3>
            <div v-for="sode in episode">
              <div v-for="inner in sode">
                <p>{{ inner }}</p>
              </div>
            </div>
          </div>
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
      id: "",
      episode: []
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
          // vince is a bo$$ and came up with this simple AF solution
          this.results = [];
          // this.episode = [];
          if (response.data.results) {
            (this.results.push(response.data.results));
          } else {
            console.log("show not available.");
          };
        }.bind(this)
      );
      console.log("HI:");
      // console.log(results);
    },

    shuffleSeason: function(thing) {
      var episode = "";
      var params = {
        id: thing.id
      };
      console.log("ID HERE: ");
      console.log(params);
      axios.post("http://localhost:3000/api/episodes", params).then(
        function(response) {
          this.episode = [];
          this.episode.push(response.data);
        }.bind(this),
        console.log(this)
      );
      console.log("BEFORE:");
      console.log(thing);
      console.log(thing.visible);
      thing.visible = !thing.visible;
      console.log("AFTER:");
      console.log(thing.visible);
    }
  },
  computed: {}
};
</script>
