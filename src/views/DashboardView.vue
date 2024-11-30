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
  let authObj = JSON.parse(user.value);
  /**
   * fetch company competence via a protected route,
   * using bearer token for authorization
   */
  const response = await fetch(
    `${SystemConfig.serverUrl}:${SystemConfig.serverPort}/api/v1/gc/competencies`,
    {
      //integrate user token to the header for authorization
      headers: { Authorization: `Bearer ${authObj.token}` },
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

/**
 * @implementation
 * the end point makes a request to the same server without the bearer
 * tokens
 *
 * @params {*} void
 * @returns
 * void
 *
 * @authors
 * @since
 * v1.0.0
 */
const unprotectedEndPoint = async () => {
  isLoading = true;

  /**
   * fetch company competence via a protected route,
   * using bearer token for authorization
   */
  const response = await fetch(
    `${SystemConfig.serverUrl}:${SystemConfig.serverPort}/api/v1/gc/competencies`,
    {
      //integrate user token to the header for authorization
      // headers: { Authorization: `Bearer ${user.token}` },
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
    // error = json.error;
    competencies.value = json;
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
      <div class="col-12">
        <div class="dashboard" v-if="user">
          <h1>This is the Dashboard</h1>

          <div class="routes">
            <div
              class="btn-group"
              role="group"
              aria-label="Basic outlined example"
            >
              <button
                type="button"
                @click="fetchCompanyCompetence"
                class="btn btn-outline-secondary"
                title="route: http://localhost:4000/api/v1/gc/competencies"
              >
                click here to get golding company competence via a protected
                route
              </button>
              <button
                type="button"
                @click="unprotectedEndPoint"
                class="btn btn-outline-secondary"
                title="route: http://localhost:4000/api/v1/gc/competencies"
              >
                click here for the same endpoint via unprotected Route
              </button>
            </div>
          </div>

          <p>{{ competencies }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.dashboard {
  width: 100%;
  min-height: 80vh;
  /* border: ridge; */
  background-image: url("../assets/gc.png");
  background-repeat: no-repeat;
  background-position: center;
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

.routes {
  margin-top: 20px;
}

h1 {
  margin-top: 20px;
}
p {
  margin-top: 20px;
}
</style>
