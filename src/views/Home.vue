<template>
  <div class="home">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Welcome To Shufflix!</h1>
        <p class="lead">Please search for a show.</p>
        <div class="form-signin">
          <input
            class="btn-block form-control"
            type="text"
            v-model="text"
            placeholder="Example: The Office"
            onfocus="this.placeholder=''"
          />
          <button
            v-on:click="search(isError)"
            class="btn btn-primary btn-block"
          >
            <i class="fas fa-search"></i>
          </button>
        </div>
      </div>
    </div>

    <div>
      <div v-for="result in results">
        <h2>Results:</h2>
        <div v-for="thing in result" class="container">
          <div class="card-body">
            <div v-html="thing.content"></div>
            <button v-model="id" v-on:click="shuffleSeason(thing)">
              Shuffle Season
            </button>
            <div v-if="thing.visible">
              <h3>You should watch episode:</h3>
              <div v-for="sode in episode">
                <div v-for="inner in sode">
                  <div v-html="inner"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div v-if="isError" style="color: red">
        <h2>We're sorry but that show isn't available</h2>
      </div>
    </div>
  </div>
</template>

<style>
.jumbotron {
  background-color: #d9d9d9;
}

.card-body {
  text-align: justify;
  border: solid black;
}

img {
  float: left;
  margin-right: 15px;
}
</style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Welcome to our app Shufflix!",
      results: [],
      text: "",
      episode: [],
      isError: false
    };
  },

  created: function() {},
  methods: {
    search: function(isError) {
      var params = {
        text: this.text
      };
      axios.post("http://localhost:3000/api/searches", params).then(
        function(response) {
          // vince is a bo$$ and came up with this simple AF
          this.results = [];
          // this.episode = [];
          this.results.push(response.data.results);
          this.isError = false;
          // console.log("LOOK HERE:");
          // console.log(this.results[0].length);
          if (this.results[0].length === 0) {
            this.isError = true;
            console.log("NO DICE");
          }
        }.bind(this)
      );
      console.log("HI:");
      console.log(this);
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
      thing.visible = !thing.visible;
    }
  }
};
</script>
