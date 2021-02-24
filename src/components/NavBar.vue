<script>
import axios from "axios";
import { inject, onBeforeMount, reactive } from "vue";

import NavItem from "../components/NavItem";


export default {
  name: "navBar",
  props: {
    sessionId: String
  },
  emits: ["logout"],
  inject: ["servicePath", "systemFeatureCode", "implementedFeatureCodes"],
  components: { NavItem },
  setup(props, { emit }) {
    const menuItems = reactive([]);
    const loggedOut = () => {
      emit("logout");
    };
    const servicePath = inject("servicePath");
    const systemFeatureCode = inject("systemFeatureCode");
    const implementedFeatureCodes = inject("implementedFeatureCodes");
    let featureCodeSelected = "";
    let featureTree = {};

    const fillMenu = (features) => {
      if (!features) return;
      Array.from(features).forEach((feature) => {
        if (implementedFeatureCodes.includes(feature.code)) {
          menuItems.push( {code : feature.code, name : feature.name, key: feature.id } )
        }
        if (feature.children) fillMenu(feature.children);
      });
    };

    const logout = () => {
      const requestConfig = { headers: { Authorization: "Bearer " + props.sessionId }};
      axios
        .get(servicePath + "/logout", requestConfig)
        .then((response) => loggedOut(response))
        .catch((error) => console.log(error));
    };
    onBeforeMount(() => {
      const setTree = (obj) => { 
        featureTree = obj;
        fillMenu(featureTree);
      };
      const requestConfig = { headers: { Authorization: "Bearer " + props.sessionId }, params: { featureCode: systemFeatureCode}};
      axios
        .get(servicePath + "/current-user/system-menu", requestConfig)
        .then((response) => setTree(response.data))
        .catch((error) => console.log(error));      
    });
    return { logout, menuItems, featureCodeSelected, featureTree };
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
          <NavItem v-for="(item, index) in menuItems" :featureTree="featureTree" :index="index" :key="item.key" :code="item.code">{{item.name}}</NavItem>
        </ul>
        <button class="btn btn-outline-danger" type="submit" @click.prevent="logout">Logout</button>
      </div>
    </div>
  </nav>

</template>