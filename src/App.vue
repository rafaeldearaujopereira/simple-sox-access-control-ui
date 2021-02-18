<script>
import Login from "./components/Login";

document.title = "Access Control v 1.0";

export default {
  name: "App",
  data () {
    return {
      sessionId: null
    }
  },
  components: { Login }
};
</script>

<template>
  <div class="text-center">
    <Login v-if="!sessionId" v-model:sessionId="sessionId" />
    {{ sessionId }}
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