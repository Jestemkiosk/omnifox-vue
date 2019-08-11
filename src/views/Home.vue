<template>
  <div id="app">
    <MainHeader />
    <Features />
    <Collage />
    <Feedback />
    <Cities v-bind:cities="cities" />
    <Footer />
  </div>
</template>

<script>
import MainHeader from "../components/MainHeader.vue"
import TopNav from "../components/Cities.vue"
import Features from "../components/Features.vue"
import Collage from "../components/Collage.vue"
import Steps from "../components/Steps.vue"
import Feedback from "../components/Feedback.vue"
import Cities from "../components/Cities.vue"
import Footer from "../components/Footer.vue"

import axios from 'axios'

export default {
    name: "app",
    components: {
        MainHeader,
        TopNav,
        Features,
        Collage,
        Steps,
        Feedback,
        Cities,
        Footer
    },
    data(){
        return{
            foxes:[

            ],
            cities:[

            ],
            sortByKeyLength: function (array, key) {
                return array.sort(function(a, b) {
                    var x = a[key].length; var y = b[key].length;
                    return ((x < y) ? -1 : ((x > y) ? 1 : 0)) * -1;
                });
            }
        }
    },
    created(){
        axios.get('http://89.68.148.28/cities/')
        .then(res => {
        this.cities = this.sortByKeyLength(res.data, 'foxes')
        console.log(this.cities)
        
        })  
        .catch(err => console.log(err))
    }
};

</script>

<style>


</style>