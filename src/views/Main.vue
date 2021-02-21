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
      console.log('entrou na clearSession')
      emit("update:sessionId", "")
    };
    return { clearSessionId };
  },
};
</script>

<template>
  <NavBar :sessionId="sessionId" @logout="clearSessionId" />
</template>