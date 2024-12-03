<script setup>
import { ref } from "vue";
import router from "../router";
import { SystemConfig } from "../modules/configurations/systemConfig";
import Header from "../components/Header.vue";

let display = ref(false);
let message = ref("");
let alertType = ref("");
let firstname = ref("");
let lastname = ref("");
let email = ref("");
let password = ref("");
let user = ref(localStorage.getItem("user"));
let isLoading = ref(false);
let error = ref("");

/**
 * @implementation
 * The signup function enables the user to signup on the application
 * and switches the user to the login form, it also setup the client
 * authentication signature using jwt token and id, to restrict access
 * to protected sections of the application at the cleient side and to
 * for the request header bearer token to server verification
 *
 * @params {*} void
 * @returns
 * void
 *
 * @authors
 * @since
 * v1.0.0
 */
async function signup() {
  isLoading = true;
  /**
   * register user using the signup route
   * route: host:/api/v1/user
   */
  const response = await fetch(
    `${SystemConfig.serverUrl}:${SystemConfig.serverPort}/api/v1/gc/user`,
    {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        firstname: firstname.value,
        lastname: lastname.value,
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
    // localStorage.setItem("user", JSON.stringify(json));

    // update loading state
    isLoading = false;

    //setup success alert
    message.value = "user created successfully";
    display.value = true;
    alertType.value = "success";

    /**
     * route user to the login form
     */
    // router.push({ name: "Login" });
  } else {
    isLoading = false;
    error = json.error;

    //setup error alert
    message.value = json.error;
    display.value = true;
    alertType.value = "danger";
  }
}
</script>

<!--
- Signup View to enable user to signup on the application
- it presents the signup form
-->
<template>
  <div class="row">
    <Header :display="display" :message="message" :alertType="alertType" />

    <div class="row">
      <div class="signup" v-if="!user">
        <div class="portlet">
          <h3>Signup Form</h3>
          <form @submit.prevent="signup">
            <div class="mb-3">
              <label for="firstname" class="form-label">Firstname</label>
              <input
                type="text"
                name="firstname"
                class="form-control"
                id="firstname"
                v-model="firstname"
                required
                placeholder="enter your firstname"
              />
            </div>

            <div class="mb-3">
              <label for="lastname" class="form-label">Lastname</label>
              <input
                type="text"
                name="lastname"
                class="form-control"
                id="lastname"
                v-model="lastname"
                required
                placeholder="enter your lastname"
              />
            </div>

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
.signup {
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
</style>
