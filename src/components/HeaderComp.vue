<template>
  <header class="d-flex justify-content-between align-items-center px-3">
    <div class="logo">
      <img  src="../assets/img/logo-boolflix.png" alt="Logo Boolflix">
    </div>
    <div class="d-flex">
      <input class="form-control mx-3" 
      placeholder="Cerca un film"
      @keyup.enter="startSearch" v-model.trim="titleToSerach" type="text" >
      <select  class="form-control"  v-model="typeToSearch" @change="startSearch">
        <option value="all">All</option>
        <option value="movie">Movie</option>
        <option value="tv">Tv</option>
      </select>
    </div>
   
  </header>
</template>

<script>
export default {
  name: 'HeaderComp',
  data(){
    return{
      titleToSerach: '',
      typeToSearch: 'all'
    }
  },
  methods:{
    startSearch(){
      this.$emit('startSearch',this.titleToSerach, this.typeToSearch);
      this.titleToSerach = '';
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/style/vars';
header{
  position: fixed;
  width: 100%;
  z-index: 999;
  top: 0;
  left: 0;
  height: 80px;
  background-image: linear-gradient(black, $bg-color);
  .logo{
    height: 100%;
    padding-top: 15px;
    img{
      height: 60%;
    }
  }
  input{
    min-width: 400px;
  }
}

</style>