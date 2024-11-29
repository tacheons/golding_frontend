<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<!--
- Root Component for the integration of various views and compoets
- Renders routed views
-->
<template>
  <div class="container text-center">
    <div class="row">
      <div class="col-12 viewport">
        <RouterView />
      </div>
    </div>
  </div>
</template>

<style scoped>
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

.viewport {
  display: flex;
  align-items: center;
  justify-content: center;
  /* border: ridge 3px; */
}

.headrow {
  border-bottom: groove 3px;
  border-color: #9e9e9e;
}

header {
  display: flex;
  place-items: center;
  /* padding-right: calc(var(--section-gap) / 2); */
}

header .wrapper {
  display: flex;
  place-items: flex-start;
  flex-wrap: wrap;
}
</style>
