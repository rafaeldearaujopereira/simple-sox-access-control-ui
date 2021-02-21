<script>
import Login from "./components/Login";
import Main from "./views/Main";

document.title = "Access Control v 1.0";

export default {
  name: "App",
  data () {
    return {
      sessionId: null,
    }
  },
  provide: {
      systemFeatureCode: 'ACCESS_CONTROL_SYS',
      servicePath: 'http://localhost:8888'
  },
  components: { Login, Main }
};
</script>

<template>
  <div class="text-center">
    <Login v-if="!sessionId" v-model:sessionId="sessionId"/>
    <Main v-if="sessionId" v-model:sessionId="sessionId"/>
  </div>
</template>

<style scoped>
html,
App,
body {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #f5f5f5;
}
</style>