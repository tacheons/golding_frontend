<script setup>
import { ref, onMounted } from "vue";
import { SystemConfig } from "../modules/configurations/systemConfig";
import router from "../router";
import Header from "../components/Header.vue";

let user = ref(localStorage.getItem("user"));
let isLoading = ref(false);
let competencies = ref("");

if (!user.value) {
  router.push({ name: "Login" });
}

/**
 * @implementation
 * Fetch company competence function, is use to make a remote
 * request to a an authenticated route for the golding company
 * list of competence or expertise.
 *
 * @params {*} void
 * @returns
 * void
 *
 * @authors
 * @since
 * v1.0.0
 */
const fetchCompanyCompetence = async () => {
  isLoading = true;

  //parse stringified json data on local storage
  user = JSON.parse(user.value);
  /**
   * fetch company competence via a protected route,
   * using bearer token for authorization
   */
  const response = await fetch(
    `${SystemConfig.serverUrl}:${SystemConfig.serverPort}/api/v1/gc/competencies`,
    {
      //integrate user token to the header for authorization
      headers: { Authorization: `Bearer ${user.token}` },
    }
  );

  // resolve json data
  const json = await response.json();
  console.log(json);

  /**
   * resolve request
   */
  if (response.ok) {
    /**
     * log competence and display the object on the dashboard
     */
    competencies.value = json;

    // update loading state
    isLoading = false;
  } else if (!response.ok) {
    isLoading = false;
    error = json.error;
  }
};
</script>

<!--
- This is the Dashboard of the application, with restricted access
- to functions and menu
-->
<template>
  <div class="row">
    <Header />

    <div class="row">
      <div class="dashboard" v-if="user">
        <h1>This is the Dashbaord</h1>
        <button class="btn btn-secondary" @click="fetchCompanyCompetence">
          get golding company competence
        </button>
        <p>{{ competencies }}</p>
      </div>
    </div>
  </div>
</template>

<style>
.dashboard {
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

h1 {
  margin-top: 20px;
}
p {
  margin-top: 20px;
}
</style>
