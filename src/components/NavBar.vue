<script>
import axios from "axios";
import { inject, onBeforeMount } from "vue";

import NavItem from "../components/NavItem";


export default {
  name: "navBar",
  props: {
    sessionId: String
  },
  emits: ["logout"],
  inject: ["servicePath", "systemFeatureCode"],
  components: { NavItem },
  setup(props, { emit }) {
    const loggedOut = () => {
      emit("logout");
    };
    const servicePath = inject("servicePath");
    const systemFeatureCode = inject("systemFeatureCode");
    let featureCodeSelected = "";
    let featureTree = {};

    const seekFeatureCode = (code, features) => {
      console.log(features)
      if (!features) return false;
      Array.from(features).forEach((feature) => {
        if (feature.code === code) return true;
        if (feature.children) return seekFeatureCode(code, feature.children);
        return false;
      });
    };
    
    let hasAccess = (code) => {
      console.log("code inside computed:" + code)
      console.log("featureTree inside computed:" + featureTree)
      console.log(featureTree)
      return seekFeatureCode(code, featureTree);     
    };

    const logout = () => {
      const requestConfig = { headers: { Authorization: "Bearer " + props.sessionId }};
      axios
        .get(servicePath + "/logout", requestConfig)
        .then((response) => loggedOut(response))
        .catch((error) => console.log(error));
    };
    onBeforeMount(() => {
      const setTree = (obj) => { featureTree = obj;  };
      const requestConfig = { headers: { Authorization: "Bearer " + props.sessionId }, params: { featureCode: systemFeatureCode}};
      axios
        .get(servicePath + "/current-user/system-menu", requestConfig)
        .then((response) => setTree(response.data))
        .catch((error) => console.log(error));      
    });
    return { logout, featureCodeSelected, featureTree, hasAccess };
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
          <NavItem v-if="hasAccess('AC_SEARCH_USER')">Users</NavItem>
          <NavItem v-if="hasAccess('AC_SEARCH_ROLE')">Roles</NavItem>
          <!--NavItem :featureTree="featureTree" code="AC_SEARCH_FEATURE">Features</NavItem>
          <NavItem :featureTree="featureTree" code="AC_REPORT_EVENT">Event Report</NavItem-->
        </ul>
        <button class="btn btn-outline-danger" type="submit" @click.prevent="logout">Logout</button>
      </div>
    </div>
  </nav>

</template>