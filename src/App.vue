<template>
  <div id="app">
    <header id="header">
      <div class="inner">
        <a href="#" class="image avatar"><img src="images/avatar.jpg" alt="" /></a>
        <h1>
          <strong>Movie App</strong>
          <li v-if="!isLoggedIn()"><router-link to="/signup">Signup</router-link></li>
          |
          <li v-if="!isLoggedIn()"><router-link to="/login">Login</router-link></li>
          |
          <li v-if="isLoggedIn()"><router-link to="/logout">Logout</router-link></li>
          |
          <router-link to="/movies">All Movies</router-link>
          |
          <router-link to="/movies/new">New Movie</router-link>
        </h1>
      </div>
    </header>

    <div class="container">
      <!-- every individual view in the views file gets interpolated here -->
      <router-view />
    </div>

    <footer id="footer">
      <div class="inner">
        <ul class="icons">
          <li>
            <a href="#" class="icon brands fa-twitter"><span class="label">Twitter</span></a>
          </li>
          <li>
            <a href="#" class="icon brands fa-github"><span class="label">Github</span></a>
          </li>
          <li>
            <a href="#" class="icon brands fa-dribbble"><span class="label">Dribbble</span></a>
          </li>
          <li>
            <a href="#" class="icon solid fa-envelope"><span class="label">Email</span></a>
          </li>
        </ul>
        <ul class="copyright"></ul>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function() {
      return localStorage.getItem("user_id");
    }
  }
};
</script>
