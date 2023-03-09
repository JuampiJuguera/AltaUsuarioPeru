<template>
  <alta-de-usuario-peru />
</template>

<script>
import AltaDeUsuarioPeru from "./components/AltaDeUsuarioPeru.vue";

export default {
  name: "App",
  components: {
    AltaDeUsuarioPeru,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-weight: 800;
}
</style>
