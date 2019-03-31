<template>
  <div id="app">
    <TestPack msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import TestPack from "./components/TestPack.vue";

export default {
  name: "app",
  components: {
    TestPack
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

@import '../node_modules/bulma/bulma.sass'
</style>
