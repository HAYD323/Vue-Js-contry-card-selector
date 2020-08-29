<template>
    <section>
        <form>
            <input v-model="filterString"
            v-bind:title="userProvidedString"
             placeholder="Search for country">
             <br />
            {{countryFilterString}}
        </form>
        <ul v-if="countries"
         class="grid-container">

            <li class="grid-item" 
            v-for="(item, index) in filterCountries(countryFilterString)" 
            v-bind:key="index"
            v-bind:iso="item.alpha3Code"
            v-on:click="toggleModel">

            <img :src="item.flag"> 
            
            </li>
        </ul>
    </section>
</template>


<script>
import countryService from  '../services/countryService';

export default {
  name: 'countriesGrid',
  data: function() {
    return {
      countries: null,
      countryFilterString: ''
    }
  },
  created: function() {
    var vm = this;
      countryService.get()
      .then(function(data){
        vm.countries = data;
      })
  },
  computed: {
      filterString: {
          get(){
              return this.countryFilterString
          },
          set(newVal){
              this.countryFilterString = this.sanitiseUserInput(newVal)
          }
      }
  },
  methods: {
      sanitiseUserInput: function(input) {
          let output = '',
              regex = /[<>'()"]/gi;
            output = input.replace(regex,'');
            console.log('sanitize: ', input, output);
          return output;
      },
      filterCountries: function(filterstring) {
          console.log("start", filterstring.length, this.countries);
          return countryService.filter(this.countries,filterstring);
      },
      toggleModel: function() {

      }
  }
}
</script>
<style scoped lang="scss">
.grid-container {

    display: flex;
    flex-direction: row;
    align-items: flex-start;
    flex-wrap: wrap;
    padding: 0;
    margin: 30px auto 0;
    width: 100%;

    .grid-item {
        width: 25%;
        height: 350px;
        display: block;
        padding: 10px;
        box-sizing: border-box;
        
        img {
            max-width: 100%;
            max-height: 100%;
            display: inline;
            text-align: center;
        }
    }
}

</style>