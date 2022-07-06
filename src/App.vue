<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <img alt="calculator logo" class="logo" src="./assets/logo.png" />
  <HelloWorld />
</template>

<style lang="scss">
@import 'bootstrap/scss/bootstrap.scss';
@import 'bootstrap-vue-3/src/styles/styles.scss';

html,
body {
  width: 100%;
  height: 100%;
  background-color: #262729;
}

#app p,
label {
  color: #a2acbd;
  font-size: 1.2rem;
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

@media (max-width: 576px) {
  .logo {
    width: 150px;
  }
}
</style>
