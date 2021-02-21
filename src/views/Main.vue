<script>
import NavBar from "../components/NavBar";

export default {
  name: "mainView",
  props: {
    sessionId: String,
  },
  inject: ["servicePath", "systemFeatureCode"],
  components: { NavBar },
  setup(props, { emit }) {
    const clearSessionId = () => {
      emit("update:sessionId", "")
    };
    return { clearSessionId };
  },
};
</script>

<template>
  <NavBar :sessionId="sessionId" @logout="clearSessionId" />
</template>