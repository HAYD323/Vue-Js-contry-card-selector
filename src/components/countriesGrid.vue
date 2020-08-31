<template>
    <section>
        <countryDetailed :item="selectedItem" v-if="showDetailed" v-on:closeModel="toggleModel('close')"></countryDetailed>
        <div v-show="!showDetailed">
            <form>
                <input v-model="filterString"
                v-on:keydown="sanitiseUserInput(event)"
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
                v-on:click="selectItem(item)">

                <img :src="item.flag"
                    :alt="item.name + '\'s Flag'"> 

                </li>
            </ul>
        </div>
    </section>
</template>


<script>
import countryService from  '../services/countryService';
import countryDetailed from './countryDetail.vue';

export default {
  name: 'countriesGrid',
  components: {
      countryDetailed
  },
  data: function() {
    return {
      countries: null,
      countryFilterString: '',
      showDetailed: false
    }
  },
  props: {
    // countries: Array
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
  created: function() {
    var vm = this;
      countryService.get()
      .then(function(data){
        vm.countries = data;
      })
  },
  methods: {
      sanitizeKeydown: function(e){
          let regex = /[<>'()"]/;
        if (regex.test(e.key)){
            e.preventDefault();
        }
      },
      sanitiseUserInput: function(input) {
          let output = '',
              regex = /[<>'()"]/gi;
            output = input.replace(regex,'');
          return output;
      },
      filterCountries: function(filterstring) {
          return countryService.filter(this.countries,filterstring);
      },
      selectItem: function(itemObj){
          this.selectedItem = countryService.filter(this.countries,itemObj)[0]; 
          this.toggleModel();         
      },
      toggleModel: function(state) {
            if (state === "close") {
                this.showDetailed = false;
            } else {
                this.showDetailed = this.showDetailed != true ? true : false;
            }
      }
  }
}
</script>
<style scoped lang="scss">
.grid-container {

    display: flex;
    flex-flow: row wrap;
    align-items: flex-start;
    padding: 0;
    margin: 30px auto 0;
    width: 100%;
    justify-content: center;

    .grid-item {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px;
        box-sizing: border-box;
        
        img {
            width: 250px;
            height: 150px;
            object-fit: cover;
            border-radius: 25px;
            border: solid thin black;
        }
    }
}

</style>