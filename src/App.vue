<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <countriesGrid ></countriesGrid>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import countriesGrid from './components/countriesGrid.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    countriesGrid
  }
}
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
</style>
