<template>
  <div id="app" class="teste">
    <div class="column is-half is-offset-one-quarter">
      <h1>Pokedex</h1>
      <input class="input is-rounded" type="text" placeholder="Busca um pokemon pelo nome" v-model="search">
      <div v-for="(pokemon, index) in pokemons" :key="index" >
        <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index + 1"/>
      </div>
    </div>
    
  </div>
</template>

<script>
  import axios from 'axios'
  import Pokemon from './components/Pokemon'

  export default {
    name: 'App',
    data() {
      return {
        pokemons: []
      }
    },
    created: function() {
      // axios.get('https://pokeapi.co/api/v2/pokemon?limit=1025&offset=0').then(response => {
      //   this.pokemons = response.data.results
      // })
       axios.get('https://pokeapi.co/api/v2/pokemon?limit=6&offset=0').then(response => {
        this.pokemons = response.data.results
      })
    },
    components: {
      Pokemon
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
  margin-top: 60px;
}
.teste {
  background: white;
}
</style>
