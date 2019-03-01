<template>
  <div class="login">
    <div class="container">
      <form v-on:submit.prevent="submit()" class="form-signin">
        <h1 class="h3 mb-3 font-weight-normal">Log In</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <input type="email" class="form-control" v-model="email" placeholder="Email Address">
        </div>
        <div class="form-group">
          <input type="password" class="form-control" v-model="password" placeholder="Password">
        </div>
        <input type="submit" class="btn btn-primary btn-block" value="Submit">
        <p class="mt-5 mb-3 text-muted">©2019 SHUFFLIX</p>
      </form>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    template: '#login-page',
    data: function() {
      return {
        email: '',
        password: '',
        errors: [],
      };
    },
    methods: {
      submit: function() {
        var params = {
          email: this.email,
          password: this.password,
        };
        axios
          .post('http://localhost:3000/api/sessions', params)
          .then(response => {
            axios.defaults.headers.common['Authorization'] = 'Bearer ' + response.data.jwt;
            localStorage.setItem('jwt', response.data.jwt);
            this.$router.push('/');
          })
          .catch(error => {
            this.errors = ['Invalid email or password.'];
            this.email = '';
            this.password = '';
          });
      },
    },
  };
</script>
