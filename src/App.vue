<template>
  <div id="app">
      
    <HeaderComp @startSearch="startSearch" /> 

    <div class="container main-wrapper">
      <MainComp v-if="movie.length > 0" titleCards="Film" :items="movie" />
      <MainComp v-if="tv.length > 0" titleCards="Serie Tv" :items="tv" /> 

      <h1 v-if="movie.length === 0 && tv.length === 0">Nessun risultato</h1>
    </div>

    

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
    this.getApi();
  },
  data(){
    return{
      apiUrl: 'https://api.themoviedb.org/3/search/',
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
    startSearch(titleToSerach, typeToSearch){
      this.movie = [];
      this.tv = [];
      this.apiParams.query = titleToSerach;
      if( titleToSerach.length > 0 ){
        if(typeToSearch === 'all'){
          this.getApi('movie');
          this.getApi('tv');
        }else{
          this.getApi(typeToSearch);
        }
        
      }
    },
    getApi(type = ''){
      let endPoint = 'https://api.themoviedb.org/3/movie/popular';
      if(type !== ''){
        endPoint = this.apiUrl + type;
      }else{
        type = 'movie';
      }
      axios.get(endPoint, {
        params: this.apiParams
      })
      .then(res => {
        console.log(res.data);
        this[type] = res.data.results;
      })
      .catch(err => {
        console.log(err);
      })
    },
  }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap.scss';
@import '~@fontsource/lato/index.css';
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import './assets/style/vars';
body{
  font-family: 'Lato', sans-serif;
  color: $font-color;
  background-color: $bg-color;
}
.main-wrapper{
  padding-top: 90px;
}
</style>
