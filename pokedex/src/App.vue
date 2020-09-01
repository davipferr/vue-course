<template>
  

  <div id="app" >
    <div class="mr-3 d-flex flex-column justify-content-center align-items-center">
        <img src="./assets/shaco.png">
        <hr>
        <h4>Pokedex</h4>
        
        <input type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input-group mb-1">
        <button type="button" class="btn btn-success" id="buscaBtn" @click="buscar">Buscar</button>

      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
      </div>  
      
    </div>
    
     
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }

  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    }) 
  },
  components:{
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
        if(this.busca == '' || this.busca ==' '){
          this.filteredPokemons = this.pokemons;
        }
         else{
           this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
         }
    }
  }
  // computed: {
  //   resultadoBusca: function(){
  //       if(this.busca == '' || this.busca ==' '){
  //         return this.pokemons;
  //       }
  //       else{
  //         return this.pokemons.filter(pokemon => pokemon.name == this.busca);
  //       }
  //   }

  // }

}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#buscaBtn{
   margin-top: 2%;
}

</style>
