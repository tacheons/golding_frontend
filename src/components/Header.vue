<script setup>
import Navbar from "../components/Navbar.vue";
</script>

<!--
- Header Component, integrate all the component and 
- menus on the header
-->
<template>
  <div class="row headrow">
    <div class="col-3">
      <header>
        <h1 class="logo">Golding Capital</h1>
      </header>
    </div>
    <div class="col-8 menu">
      <header>
        <Navbar />
      </header>
    </div>
  </div>
  <!-- 
    <div class="row alert-row">
      <div class="alert alert-success z-3" role="alert">
        A simple success alert—check it out!
      </div>
    </div> -->
</template>

<style>
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
