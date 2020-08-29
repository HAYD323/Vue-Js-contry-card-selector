<template>
    <section>
        <div class="flag">

        </div>
        <div class="text-content">

        </div>
    </section>
</template>


<script>
import countryService from  '../services/countryService';

export default {
  name: 'HelloWorld',
  data: function() {
    return {
      countries: null
    }
  },
  props: {
    msg: String
  },
  created: function() {
    var vm = this;
      countryService.get()
      .then(function(response){
        console.log(response, vm);
        vm.countries = response;
      })
  }
}
</script>