<template>
    <section class="detailed-view" v-on:click="$emit('closeModel')">
        <div class="close-btn" v-on:click="$emit('closeModel')">X</div>

        <div class="content-container">
            <div class="flag">
                <img v-bind:src="item.flag">
            </div>
            <div class="text-content">
                <h1 class="title">{{item.name}}</h1>
                <ul>
                        <li v-for="(value, key) in item"
                            v-bind:class="key"
                            v-bind:key="key">
                            {{key}} : {{value}}
                            </li>
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

        .close-btn {
            position: absolute;
            right: 2%;
            top: 2%;
            cursor: pointer;
        }

        .content-container {
            position: absolute;
            top: 50%;
            left: 50%;
            background-color: gray;
            overflow: hidden;
            transform: translate(-50%, -50%);
            width: 90%;
            height: 90%;
            border-radius: 20px;
            display: flex;
            align-items: center;
            flex-flow: column nowrap;
        }
        

        .flag img {
            width: 350px;
            height: 200px;
        }
    }
</style>