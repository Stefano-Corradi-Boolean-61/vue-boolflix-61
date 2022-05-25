<template>
  <div id="app">
      
    <HeaderComp @startSearch="startSearch" /> 

    <MainComp titleCards="Film" :items="movie" />
    <!-- <MainComp titleCards="Serie Tv" /> -->

  </div>
</template>

<script>

import HeaderComp from './components/HeaderComp.vue';
import MainComp from './components/MainComp.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    HeaderComp,
    MainComp
  },
  mounted(){
   // this.getApi();
  },
  data(){
    return{
      apiUrl: 'https://api.themoviedb.org/3/search/movie',
      apiParams:{
        api_key: '1b3eb153fce73eb6b953f7d515b2dc1d',
        language: 'it-IT',
        query: '',
      },
      movie:[],
      tv:[]
    }
  },
  methods:{
    startSearch(titleToSerach){
      this.apiParams.query = titleToSerach;
      if( titleToSerach.length > 0 )this.getApi();
    },
    getApi(){
      axios.get(this.apiUrl, {
        params: this.apiParams
      })
      .then(res => {
        console.log(res.data);
        this.movie = res.data.results;
      })
      .catch(err => {
        console.log(err);
      })
    }
  }
}
</script>

<style lang="scss">

</style>
