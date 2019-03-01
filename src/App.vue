<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Shufflix</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-item nav-link" <router-link to="/">Home </router-link></a>
          <a class="nav-item nav-link" <router-link to="/signup">Signup </router-link></a>
          <a class="nav-item nav-link" <router-link to="/login">Login </router-link></a>
          <a class="nav-item nav-link" <router-link to="/logout">Logout </router-link></a>
        </div>
      </div>
    </nav>
  </nav>

    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.form-signin {
  max-width: 400px;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
}

.card {
  display: block;
  flex-direction: column;
}
</style>