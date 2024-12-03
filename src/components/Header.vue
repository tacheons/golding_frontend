<script setup>
import { ref, toRefs } from "vue";
import Navbar from "../components/Navbar.vue";

const props = defineProps({
  message: String,
  display: Boolean,
  alertType: String,
});

// let { display } = toRefs(props);

// console.log("display = ", display.value);

// if (display.value) {
//   setTimeout(() => {
//     display.value = false;Y
//   }, 10000);
// }
</script>

<!--
- Header Component, integrate all the component and 
- menus on the header
-->
<template>
  <div>
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

    <div class="row alert-row">
      <div
        v-if="display && alertType == 'success'"
        class="alert alert-success z-3"
        role="alert"
      >
        {{ message }}
      </div>
      <div
        v-if="display && alertType == 'danger'"
        class="alert alert-danger z-3"
        role="alert"
      >
        {{ message }}
      </div>
    </div>
  </div>
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
