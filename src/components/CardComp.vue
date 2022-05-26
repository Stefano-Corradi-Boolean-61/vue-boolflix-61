<template>
  <div class="sc-card">

    <flip-flop-card :elevation="8" direction="horizontal" width="300">
      <template slot="back">
        <div class="basic-card inner">
          <img v-if="cardData.poster_path"
          class="img-fluid"
          :src="`https://image.tmdb.org/t/p/w342/${cardData.poster_path}`" 
          :alt="cardData.original_title || cardData.original_name">
          <div v-else 
          class="placeholder-poster d-flex justify-content-center align-items-center p-3 text-center" >{{cardData.original_title || cardData.original_name}}</div>
        </div>
      </template>
      <template slot="front">
        <div class="basic-card inner p-2">

            <div class="top">
              <h3>{{cardData.title || cardData.name}}</h3>
              <h4>{{cardData.original_title || cardData.original_name}}</h4>
            </div>
            
            <img class="flag" v-if="flags.includes(cardData.original_language)" 
                :src="require(`../assets/img/${cardData.original_language}.png`)" alt="">
            <p v-else>Lingua: {{cardData.original_language}}</p>
            <div>
              
              <!-- stampo le stelline piene -->
              <i 
                v-for="i in Math.floor(Math.round(cardData.vote_average)/2)"
                :key="`a${i}`"
                class="fa-star fa-solid"></i>

              <!-- stampo la mezza stella -->
              <i v-if="Math.round(cardData.vote_average) % 2" class="fa-solid fa-star-half-stroke"></i> 
              
              <!-- stampo le stelline vuote
                // la differenza di 5 meno stelle piene - modulo 2 del voto reale arrotondato
              -->
              <i 
                v-for="i in (5 - Math.floor(Math.round(cardData.vote_average)/2) - (Math.round(cardData.vote_average) % 2) )"
                :key="`b${i}`"
                class="fa-star fa-regular"></i>

              
            </div>

            <p class="overview">
              {{cardData.overview}}
            </p>

          
          
        </div>
      </template>
  </flip-flop-card>

    <!-- <h3>{{cardData.title || cardData.name}}</h3>
    <h4>{{cardData.original_title || cardData.original_name}}</h4>
    <img class="flag" v-if="flags.includes(cardData.original_language)" 
        :src="require(`../assets/img/${cardData.original_language}.png`)" alt="">
    <p v-else>Lingua: {{cardData.original_language}}</p> -->

  <!-- STELLINE -->
      <!-- <i class="fa-solid fa-star"></i>
      <i class="fa-regular fa-star"></i>  
    <p>{{cardData.vote_average}}</p> -->
    
  </div>
</template>

<script>
import FlipFlopCard from "vue-flip-flop-card";
export default {
  name: 'CardComp',
  components:{
    FlipFlopCard
  },
  data(){
    return{
      flags:['it','en']
    }
  },
  props:{
    cardData: Object
  }
}
</script>

<style lang="scss" scoped>

.sc-card{
  flex-basis: 25%;
  margin-bottom: 30px;
  .flag{
    width: 30px;
  }
  .inner{
    height: 100%;
    background-color: black;
    .top{
      min-height: 35%;
    }
  }
  .overview{
    height: 50%;
    overflow-y: auto;
  }
  .placeholder-poster{
    height: 100%;
    font-size: 1.5rem;
  }
}
</style>