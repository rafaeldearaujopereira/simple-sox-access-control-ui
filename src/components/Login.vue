<script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";

import axios from "axios";
import querystring from "querystring";

export default {
  name: "login-form",
  data() {
    return {
      username: "",
      password: "",
      externalSessionId: "",
      errorMessage: null,
    };
  },
  setup() {
    const loggedIn = (response) => {
      if (response.data) {
        console.log(response.data);
      }
    };

    const submitForm = (user, pass) => {
      const credentials = { username: user, password: pass };
      axios
        .post("http://localhost:8888/login", querystring.stringify(credentials))
        .then((response) => loggedIn(response))
        .catch((error) => console.log(error));
    };
    return { submitForm, v$: useVuelidate() };

  },
  validations() {
    return {
      username: { required },
      password: { required },
    };
  },
};
</script>

<template>
  <main class="form-signin">
    <form @submit.prevent="submitForm(username, password)">
      <h1 class="h3 mb-3 fw-normal">Login @ Access Control</h1>

      <label for="login" class="visually-hidden">Username</label>
      <input
        type="text"
        v-model="username"
        class="form-control"
        placeholder="Username"
        required
        autofocus
      />
      <label for="password" class="visually-hidden">Password</label>
      <input
        type="password"
        v-model="password"
        class="form-control"
        placeholder="Password"
        required
      />

      <button class="w-100 btn btn-md btn-primary" type="submit">
        Sign in
      </button>
      <div v-if="errorMessage">{{ errorMessage }}.</div>
    </form>
  </main>
</template>

<style scoped>
html,
Login,
body {
  height: 100%;
}

.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}
.form-signin .checkbox {
  font-weight: 400;
}
.form-signin .form-control {
  position: relative;
  box-sizing: border-box;
  height: auto;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
