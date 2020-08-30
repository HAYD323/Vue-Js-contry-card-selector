<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <countriesGrid :countries="propCountries"></countriesGrid>    
    <countryDetail :countries="propCountries" v-if="showDetailed"></countryDetail>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import countriesGrid from './components/countriesGrid.vue'
import countryDetail from './components/countryDetail.vue'
import countryService from  './services/countryService';

export default {
  name: 'App',
  components: {
    // HelloWorld
    countriesGrid,
    countryDetail
  },
  data: function() {
    return {
      showDetailed: true
    }
  },
  created: function() {
    var vm = this;
      countryService.get()
      .then(function(data){
        vm.countries = data;
      })
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
