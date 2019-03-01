<template>
  <div class="home">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Welcome To Shufflix!</h1>
        <p class="lead">Search for a show.</p>
        <div class="form-signin">
          <input class="btn-block form-control" type="text" v-model="text" placeholder="Example: The Office" onfocus="this.placeholder=''">
          <button v-on:click="search(isError)" class="btn btn-primary btn-block"><i class="fas fa-search"></i></button>
        </div>
      </div>
    </div>

    <div>
      <!-- <p>{{ results }}</p> -->
      <div v-for="result in results">
        <h2>Results:</h2>
        <div v-for="thing in result" class="container" v-on:click="shuffleSeason(thing)">

          <div class="card-body">
            <p class="card-header">{{ thing.title }}</p>
            <img v-bind:src="thing.pic" class="card-body">
          </div>

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

      <div v-if="isError" style="color: red">
        <h2>We're sorry but that show isn't available</h2>
      </div>
    </div>

  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      message: 'Welcome to our app Shufflix!',
      results: [],
      text: '',
      id: '',
      episode: [],
      isError: false,
    };
  },

  created: function() {},
  methods: {
    search: function(isError) {
      var params = {
        text: this.text,
      };
      axios.post('http://localhost:3000/api/searches', params).then(
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
            console.log('NO DICE');
          }
        }.bind(this)
      );
      console.log('HI:');
      // console.log(results);
    },

    shuffleSeason: function(thing) {
      var episode = '';
      var params = {
        id: thing.id,
      };
      console.log('ID HERE: ');
      console.log(params);
      axios.post('http://localhost:3000/api/episodes', params).then(
        function(response) {
          this.episode = [];
          this.episode.push(response.data);
        }.bind(this),
        console.log(this)
      );
      console.log('BEFORE:');
      console.log(thing);
      console.log(thing.visible);
      thing.visible = !thing.visible;
      console.log('AFTER:');
      console.log(thing.visible);
    },
  },
  computed: {},
};
</script>
