<template>
  <div class="home">
    <h1 class="title text-center">Test Pokédex</h1> 
    <p class="text-center">
      Esta es una prueba utilizando el API no oficial de Pokémon <a href="https://pokeapi.co/">PokeApi</a>, 
      mostrando la información básica de cada Pokémon como el tipo, peso y habilidades.
    </p>
    <h4 class="text-center">Ejemplos</h4>
      <DexList :list="pokemon"/>
  </div>
</template>

<script>
// @ is an alias to /src
//componentes
import DexList from '../components/DexList';

import data from "../assets/mock-up-pokemon.json";


export default {
  name: 'Home',
  components: {
    DexList
    
  },
  data() {
    return {
      pokemon: data.pokemon,
    }
  }
}
</script>

<style>
  .home {
    padding: 0 4rem;
    margin: 0 2rem;
  }

  .title {
    display: block;
    margin: 1.5rem auto;
  }
</style>
