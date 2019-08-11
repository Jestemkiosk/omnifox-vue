<template>
    <div>
        <CitiesHeader />
            <div class="cities">
                <h1>API Endpoint: http://api.wmetryka.pl/cities</h1>
                <div class="row" v-bind:key="cities.index" v-for="cities in chunkedCities">
                    <City v-bind:city="city" v-bind:key="city.id" v-for="city in cities"/>
                </div>
            </div>
        <Footer />
    </div>
</template>

<script>
import City from '../components/City.vue'
import CitiesHeader from "../components/CitiesHeader.vue"
import Footer from "../components/Footer.vue"

import axios from 'axios'
import chunk from 'chunk'

export default {
    name: "CitiesView",
    components: {
        CitiesHeader,
        Footer,
        City
    },
    data(){
        return{
            cities: [

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
        
        })
        .catch(err => console.log(err))
    },
    computed: {
        chunkedCities(){
            return chunk(this.cities, 4)
        }
    }
}
</script>

<style scoped>
.cities{
    margin: 50px 0 50px 0px;
}

h1{
    color:black;
    text-align: center;
    font-size: 0.7em;
    margin: 20px;
}

@media only screen and (max-width: 1023px){
  .cities{
      margin: 0px;
  }
}
</style>