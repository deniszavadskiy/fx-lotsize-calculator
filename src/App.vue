<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <img alt="calculator logo" class="logo" src="./assets/logo.png" />
  <HelloWorld/>
</template>

<style>
html,
body {
  width: 100%;
  height: 100%;
}

body {
  background: linear-gradient(
    340deg,
    rgba(155, 176, 255, 1) 0%,
    rgba(226, 250, 255, 1) 100%
  );
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.logo {
  width: 250px;
  margin: 1rem;
}

</style>
