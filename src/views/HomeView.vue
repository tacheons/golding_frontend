<script setup>
import Header from "../components/Header.vue";
</script>

<!--
- Home page, this is the landing page of the application
- with no restricted functions and menues
-->
<template>
  <div class="row">
    <Header />

    <div class="row">
      <div class="home">
        <h1>This is the Home page</h1>
      </div>
    </div>
  </div>
</template>

<style>
.home {
  width: 100%;
  min-height: 100vh;
  /* border: ridge; */
}

.headrow {
  border-bottom: groove 3px;
  border-color: #9e9e9e;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}
.menu {
  display: flex;
  align-items: center;
  justify-content: center;
  /* border: ridge 3px; */
}
</style>
