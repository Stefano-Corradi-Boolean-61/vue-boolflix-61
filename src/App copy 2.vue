<template>
  <div id="app">
      
    <HeaderComp @startSearch="startSearch" /> 

    <MainComp v-if="movie.length > 0" titleCards="Film" :items="movie" />
    <MainComp v-if="tv.length > 0" titleCards="Serie Tv" :items="tv" /> 

    <h1 v-if="movie.length === 0 && tv.length === 0">Nessun risultato</h1>

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
      apiUrlMovie: 'https://api.themoviedb.org/3/search/movie',
      apiUrlTv: 'https://api.themoviedb.org/3/search/tv',
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
      if( titleToSerach.length > 0 ){
        this.getApiMovie();
        this.getApiTv();
      }
    },
    getApiMovie(){
      axios.get(this.apiUrlMovie, {
        params: this.apiParams
      })
      .then(res => {
        console.log(res.data);
        this.movie = res.data.results;
      })
      .catch(err => {
        console.log(err);
      })
    },
    getApiTv(){
      axios.get(this.apiUrlTv, {
        params: this.apiParams
      })
      .then(res => {
        console.log(res.data);
        this.tv = res.data.results;
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
