<script setup>
import { ref } from "vue";
import { SystemConfig } from "../modules/configurations/systemConfig";
import router from "../router";
import Header from "../components/Header.vue";

let display = ref(false);
let message = ref("");
let alertType = ref("");
let email = ref("");
let password = ref("");
let user = ref(localStorage.getItem("user"));
let isLoading = ref(false);
let error = ref("");

/**
 * @implementation
 * The login function enables user to login to the application and
 * interact with the protected sections of the application.
 * it authenticates with the server and registers the client authentication
 * data, use for subsequent request with the server.
 *
 * @params {*} void
 * @returns
 * void
 *
 * @authors
 * @since
 * v1.0.0
 */
async function login() {
  isLoading = true;
  /**
   * authenticate user with the server
   * route: host:/api/v1/login
   */
  const response = await fetch(
    `${SystemConfig.serverUrl}:${SystemConfig.serverPort}/api/v1/gc/login`,
    {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        email: email.value,
        password: password.value,
      }),
    }
  );
  const json = await response.json();
  console.log(json);

  /**
   * resolve request
   */
  if (response.ok) {
    // save the user to local storage
    localStorage.setItem("user", JSON.stringify(json));
    user.value = localStorage.getItem("user");

    // update loading state
    isLoading = false;

    /**
     * route user to the dashboard
     */
    router.push({ name: "Dashboard" });
    // window.location.href = window.location.origin + "/bashboard";
  } else if (!response.ok) {
    isLoading = false;
    error = json.error;

    message.value = json.error;
    display.value = true;
    alertType.value = "danger";
  }

  /**
   * clear the form inputs
   */
  email.value = "";
  password.value = "";
}
</script>

<!--
- Login View to enable user to login to the application
- with user name and password
-->
<template>
  <div class="row">
    <Header :display="display" :message="message" :type="alertType" />

    <div class="row">
      <div class="login" v-if="!user">
        <div class="portlet">
          <h3>Login Form</h3>
          <form @submit.prevent="login">
            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input
                type="email"
                name="email"
                class="form-control"
                id="email"
                v-model="email"
                required
                placeholder="name@example.com"
              />
            </div>

            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input
                type="password"
                name="password"
                class="form-control"
                id="password"
                v-model="password"
                required
              />
            </div>
            <div class="mb-3">
              <button class="btn btn-secondary" type="submit">
                <span v-if="!isLoading">Submit</span>
                <span v-if="isLoading">
                  <span
                    class="spinner-border spinner-border-sm"
                    aria-hidden="true"
                  ></span>
                  <span role="status"> Loading...</span>
                </span>
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.login {
  justify-items: center;
  width: 100%;
  min-height: 100vh;
  /* border: ridge; */
}
.form-label {
  float: left;
}
.portlet {
  margin-top: 20px;
  width: 30vw;
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
