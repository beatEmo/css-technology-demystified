<template>
  <div id="app">
    <scroll-tab v-if="false" />
    <d-card v-if="true" />
  </div>
</template>

<script>
import scrollTab from "@/components/scroll-tab.vue";
import dCard from "@/components/d-card.vue";

export default {
  name: "App",
  components: { scrollTab, dCard }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html,
body {
  display: flex;
  justify-content: center;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
  font-size: 16px;
  font-family: Arial, Helvetica, sans-serif;
  background-color: #14161f;
}
</style>
