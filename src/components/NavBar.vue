<script>
import axios from "axios";
import { inject } from "vue";

export default {
  name: "navBar",
  props: {
    sessionId: String,
  },
  emits: ["logout"],
  inject: ["servicePath", "systemFeatureCode"],
  setup(props, { emit }) {
    const loggedOut = () => {
      emit("logout");
    };
    const servicePath = inject("servicePath");
    let featureCodeSelected = "";
    let featureTree = {};
    let requestConfig = {
      headers: { Authorization: "Bearer " + props.sessionId }
    };
    const logout = () => {
      axios
        .get(servicePath + "/logout", requestConfig)
        .then((response) => loggedOut(response))
        .catch((error) => console.log(error));
    }
    return { logout, featureCodeSelected, featureTree };
  },
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light p-1">
    <div class="container-fluid">
      <a class="navbar-brand mb-0 h1" href="#">
          <img src="../assets/logo.png" alt="" width="30" height="30" class="d-inline-block align-top">
          Access Control
      </a>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item"><a class="nav-link active" aria-current="page" href="#">Users</a></li>
          <li class="nav-item"><a class="nav-link" href="#">Roles</a></li>
          <li class="nav-item"><a class="nav-link" href="#">Features</a></li>
          <li class="nav-item"><a class="nav-link" href="#">Event Report</a></li>
        </ul>
        <button class="btn btn-outline-danger" type="submit" @click.prevent="logout">Logout</button>
      </div>
    </div>
  </nav>

</template>