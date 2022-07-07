<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <div class="logo"> </div>
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
  text-align: left;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-flow: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  padding: 2rem 1rem;
}

.logo {
  background: url("./assets/logo.png") center no-repeat;
  background-size: contain;
  width: 100%;
  height: 100%;
  max-width: 250px;
}

</style>
