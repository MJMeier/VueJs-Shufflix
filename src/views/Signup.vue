<template>
  <div class="signup">
    <div class="container">
      <form v-on:submit.prevent="submit()" class="form-signin">
        <h1 class="h3 mb-3 font-weight-normal">Sign Up</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <input type="text" class="form-control" v-model="name" placeholder="Name">
        </div>
        <div class="form-group">
          <input type="email" class="form-control" v-model="email" placeholder="Email Address">
        </div>
        <div class="form-group">
          <input type="password" class="form-control" v-model="password" placeholder="Password">
        </div>
        <div class="form-group">
          <input type="password" class="form-control" v-model="passwordConfirmation" placeholder="Confirm Password">
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
  data: function() {
    return {
      name: '',
      email: '',
      password: '',
      passwordConfirmation: '',
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
      };
      axios
        .post('http://localhost:3000/api/users', params)
        .then(response => {
          this.$router.push('/login');
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
