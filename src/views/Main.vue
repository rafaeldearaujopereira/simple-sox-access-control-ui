<script>
import { useRouter } from "vue-router";
import NavBar from "../components/NavBar";

export default {
  name: "mainView",
  props: {
    sessionId: String,
  },
  inject: ["servicePath", "systemFeatureCode"],
  setup(props, { emit }) {
    const router = useRouter()
    const showView = (targetView) => {
      console.log("/" + targetView);
      router.push("/" + targetView);
    };
    const clearSessionId = () => {
      emit("update:sessionId", "");
    };
    return { clearSessionId, showView };
  },
  components: { NavBar },
};
</script>

<template>
  <NavBar
    :sessionId="sessionId"
    @logout="clearSessionId"
    @open-and-navigate-to="showView($event)"
  />
  <router-view></router-view>
</template>