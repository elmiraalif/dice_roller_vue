<template>
  <div class="panel">
    <!-- This wrapper keeps both players -->
    <Game />
  </div>
</template>
<script>
import Game from "./Game";
export default {
  name: "Panel",
  components: {
    Game
  }
};
</script>
<style scoped>
/* I want the styles on this page only applies to the panel (scoped)  */
.panel {
  width: 1000px;
  height: 600px;
  background: #1d2540;
  border-radius: 10px;
  text-align: center;
}
</style>