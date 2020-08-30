<template v-if="showDetailed">
    <section class="detailed-view">
        <div class="flag">
            <img v-bind:src="this.item.flag">
        </div>
        <div class="text-content">
            <h1 class="title">{{this.item.name}}</h1>
            <ul>
                    <li v-for="(value, key) in item"
                        v-bind:class="key"
                        v-bind:key="key">
                        {{value}}
                        </li>
            </ul>
        </div>
    </section>
</template>


<script>
import countryService from  '../services/countryService';

export default {
  name: 'countryDetailed',
  data: function() {
    return {
        item: {flag:'test.png'},
        countries: null,
        alpha3code: 'IMN'
    }
  },
  props: {
    countries: Object
  }
}
</script>

<style scoped lang="scss">
.detailed-view{
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: gray;
}
</style>