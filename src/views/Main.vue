<script>
import { defineAsyncComponent, reactive } from 'vue';
import NavBar from "../components/NavBar";

export default {
  name: "mainView",
  props: {
    sessionId: String,
  },
  inject: ["servicePath", "systemFeatureCode"],
  setup(props, { emit }) {
    const selectedComponent = reactive({});
    let iComponent = 0;
    let AsyncComponent = null;
    const showView = (targetView) => {
      console.log(targetView + " " + AsyncComponent)
      selectedComponent.value = targetView
      AsyncComponent = () => defineAsyncComponent(() => import(selectedComponent.value))
      console.log(AsyncComponent)
      iComponent++;
    }
    const clearSessionId = () => {
      emit("update:sessionId", "")
    };
    return { clearSessionId, showView, AsyncComponent, iComponent };
  },
  components: { NavBar }
};
</script>

<template>
  <NavBar :sessionId="sessionId" @logout="clearSessionId" @open-and-navigate-to="showView($event)" />
  <component :is="AsyncComponent" key="iComponent"></component>
</template>