<script>
import NavBar from "../components/NavBar";
import Feature from './Feature';

export default {
  name: "mainView",
  props: {
    sessionId: String,
  },
  inject: ["servicePath", "systemFeatureCode"],
  setup(props, { emit }) {
    const showView = (targetView) => {
      console.log("/" + targetView);
    };
    const clearSessionId = () => {
      emit("update:sessionId", "");
    };
    return { clearSessionId, showView };
  },
  components: { NavBar, Feature },
};
</script>

<template>
  <NavBar
    :sessionId="sessionId"
    @logout="clearSessionId"
    @open-and-navigate-to="showView($event)"
  />
  <Feature />
</template>