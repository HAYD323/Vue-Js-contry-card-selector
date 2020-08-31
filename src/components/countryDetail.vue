<template>
    <section class="detailed-view" >
        <div class="model-background" @click="$emit('closeModel')" >
            <div class="close-btn"><strong>X</strong></div>
        </div>

        <div class="content-container" v-if="item">
            <div class="flag">
                <img v-bind:src="item.flag">
            </div>
            
            <h1 class="title">{{item.name}}</h1>
            
            <div class="text-content">
                <p v-if="item.capital"><strong>Capital:</strong> {{item.capital}}</p>
                <p v-if="item.population"><strong>Population:</strong> {{formatNumber(item.population)}}</p>
                <p v-if="item.alpha3Code"><strong>Alpha3 Code:</strong> {{item.alpha3Code}}</p>
            </div>

                <h3 class="sub-title" v-if="item.languages">Languages:</h3>
            <div class="text-content" v-if="item.languages">
                <p v-for="(value, key) in item.languages[0]"
                            v-bind:class="key"
                            v-bind:key="key">
                            <strong>Language {{key}}:</strong> {{value}}</p>
            </div>

                <h3 class="sub-title" v-if="item.currencies">Currencies:</h3>
            <div class="text-content" v-if="item.currencies">
                <p v-for="(value, key) in item.currencies[0]"
                            v-bind:class="key"
                            v-bind:key="key">
                            <strong>Currency {{key}}:</strong> {{value}}</p>
            </div>

            <div class="text-container">
                <ul>
                        
                </ul>
            </div>
        </div>
    </section>
</template>


<script>
// import countryService from  '../services/countryService';

export default {
  name: 'countryDetailed',
  data: function() {
    return {
        // item: {flag:'test.png'},
        // alpha3code: 'IMN'
    }
  },
  props: {
    item: Object
  },
  methods: {
    formatNumber: function(num) {
            return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
        }
  }
}
</script>

<style scoped lang="scss">
.detailed-view {
    height: 100vh;
    width: 100vw;
    position: absolute;
    top: 0;
    left: 0;

        
        .model-background{
            width: 100%;
            height: 100vh;
            cursor: pointer;
        
        
                .close-btn {
                    position: absolute;
                    right: 2%;
                    top: 2%;
                    cursor: pointer;
                }
        }


        .content-container {
            position: absolute;
            top: 50%;
            left: 50%;
            background-color: lightgray;
            overflow: hidden;
            transform: translate(-50%, -50%);
            width: 90%;
            height: 90%;
            border-radius: 20px;
            display: flex;
            align-items: center;
            flex-flow: column nowrap;


            .text-content {
                width: 90%;
                display: flex;
                flex-flow: wrap row;
                justify-content: space-evenly;

                p {
                    margin-left: 5px;
                    margin-right: 5px;
                }
            }
        
        
            .flag {
                margin-top: 30px;    
                
                 img {
                    width: 100%; 
                    max-width: 350px;
                    max-height: 200px;
                }
            }
        }
        

    }
</style>