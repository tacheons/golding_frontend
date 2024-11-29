<script setup>
import { RouterLink, RouterView } from "vue-router";
import { ref } from "vue";
import router from "../router";

let user = ref(localStorage.getItem("user"));

/**
 * @implementation
 * Enables the user to logout of the application
 * It also destroys the client authentication data
 * that is store locally with user.
 *
 * @params {*} void
 * @returns
 * void
 *
 * @authors
 * @since
 * v1.0.0
 */
function logout() {
  localStorage.removeItem("user");
  user.value = "";

  router.push({ name: "Login" });
}
</script>

<!--
- Navbar for the Menu Listing and navigation
- It has both restricted and unrestricted menus
- that is resolve by user variable before and after authentication
-->
<template>
  <nav>
    <!-- logged in users -->
    <div v-if="user">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/dashboard">Dashboard</RouterLink>
      <button class="btn btn-secondary" @click="logout">Logout</button>
    </div>

    <!-- logged out users -->
    <div v-else>
      <RouterLink to="/login">Login</RouterLink>
      <RouterLink to="/signup">Signup</RouterLink>
    </div>
  </nav>
</template>

<style>
nav {
  display: flex;
  align-items: center;
}
nav h1 {
  margin-right: auto;
  margin-bottom: 0;
}
nav a {
  margin-left: 16px;
  color: white;
}
nav button {
  margin-left: 16px;
}
nav a.router-link-exact-active {
  color: #0ec58e;
}
nav + p {
  margin-top: 0;
  margin-bottom: 30px;
}
</style>
