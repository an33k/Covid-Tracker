<template>
<main v-if="!loading" >
  <DataTitle :text="title" :dateData="dateData"/>
  <DataBoxes :stats="stats" class="container"/>
</main>
<main class="flex flex-col align-center justify-center text-center" v-else>
  <div class="text-gray-500 text-3xl mt-10 mb-6">
    Fetching Data
  </div>
  <img :src="loadingImage" class="w-24 m-auto" alt="">

</main>

</template>

<script>

import DataTitle from '../components/DataTitle.vue'
import DataBoxes from '../components/DataBoxes.vue'
// @ is an alias to /src


export default {
  name: 'Home',
  data(){
    return{
      loading: true,
      title: 'Global',
      dateData:'',
      stats: {},
      countries:[],
      loadingImage: require('../assets/hourglass.gif')

    }
  },
  methods:{
    async fetchCovidData(){
      const response = await fetch('https://api.covid19api.com/summary')
      const data = await response.json()
      return data

    }
  },
  components: {
    DataTitle,
    DataBoxes
    
  },
  async created(){
    const data = await this.fetchCovidData()
    this.dateData = data.Date
    this.stats = data.Global
    this.countries = data.countries
    this.loading = false
  }
  
    } 
     
</script>

<style>
.container{
  display: inline-block;
  justify-content: center;
  padding: 2rem;
}
</style>
