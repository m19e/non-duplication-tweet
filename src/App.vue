<template>
  <div id="app">
    <OhishiIzumiSuki msg="大石泉すき" />
  </div>
</template>

<script>
import OhishiIzumiSuki from "./components/OhishiIzumiSuki.vue";

export default {
  name: "app",
  components: {
    OhishiIzumiSuki,
  },
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  text-align: center;
  /* color: #2c3e50; */
  /* margin-top: 60px; */
}
</style>
