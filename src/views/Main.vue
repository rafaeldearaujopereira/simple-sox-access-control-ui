<script>
import { computed, defineAsyncComponent, reactive } from 'vue';
import NavBar from "../components/NavBar";

export default {
  name: "mainView",
  props: {
    sessionId: String
  },
  inject: ["servicePath", "systemFeatureCode"],
  setup(props, { emit }) {
    const selectedComponent = reactive({});
    const dynamicComponent = computed(() => {
      if (selectedComponent) {
        return defineAsyncComponent(() => import(`./${selectedComponent.value}`))
      } else {
        return null
      }
    })
    const showView = (targetView) => {
      console.log(targetView + " " + selectedComponent)
      selectedComponent.value = targetView
      console.log(targetView + " " + selectedComponent)
    }
    const clearSessionId = () => {
      emit("update:sessionId", "")
    };
   return { clearSessionId, showView, dynamicComponent };
  },
  components: { NavBar }
};
</script>

<template>
  <NavBar :sessionId="sessionId" @logout="clearSessionId" @open-and-navigate-to="showView($event)" />
  <component :is="dynamicComponent"></component>
</template>