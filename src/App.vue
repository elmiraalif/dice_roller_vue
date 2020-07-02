<template>
  <div id="app">
    <!-- Panel is a container where all the game happens inside -->
    <Panel />
  </div>
</template>

<script>
import Panel from "./components/Panel.vue";

export default {
  name: "App",
  // The only component used in App
  components: {
    Panel
  }
};
</script>

<style>
/* These are the general styles regarding the entire page */
@import url("https://fonts.googleapis.com/css2?family=Muli:wght@300;500&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  background-color: #242e4c;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Muli", sans-serif;
  color: #8c8ca4;
}
</style>
