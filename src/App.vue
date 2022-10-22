<template>
  <div id="app">
      <div class="column is-half is-offset-one-quarter">
        <img src="./assets/logo_rnd.png">
        <h4 class="is-size-5">Pokedex</h4>
        <input class="input is-rounded" type="text" placeholder="Buscar por nome" v-model="busca">
        <button class="button is-fullwidth is-info is-rounded" id="btnBuscar" @click="buscar">Buscar</button>
        <div v-for="(poke,index) in filtroPokemons" :key="poke.url">
          <PokemonComp :name="poke.name" :url="poke.url" :num="index+1"/>
        </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import PokemonComp from "./components/PokemonComp.vue";

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      filtroPokemons: [],
      busca: ''
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filtroPokemons = res.data.results;
    })
  },
  components: {
    PokemonComp
  },
  methods: {
    buscar: function() {
      this.filtroPokemons = this.pokemons;
      if (this.busca == '' || this.busca == ' ' ) {
        this.filtroPokemons = this.pokemons;
      }else {
        this.filtroPokemons = this.pokemons.filter(pokemom => pokemom.name == this.busca);
      }
    }
  }
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(246, 246, 250);
}

#btnBuscar {
  margin-top: 2%;
}

</style>
