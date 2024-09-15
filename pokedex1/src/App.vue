<template>
  <div class="app">
    <img src=".assets/img/be5185a1fd0db1dfeb4c71610c19d6af.png">
    <h1>¿Quién es ese Pokémon?</h1>
    <p>Pokemones descubiertos: {{ contadorDescubiertos }}</p>
    <div class="pokemon-grid">
      <CartaPokemon 
        v-for="(pokemon, indice) in pokemones"
        :key="indice" 
        :pokemon="pokemon"
        @pokemon-descubierto="onPokemonDescubierto"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CartaPokemon from './components/CartaPokemon.vue';

export default {
  data() {
    return {
      pokemones: [],
      contadorDescubiertos: 0,
    };
  },
  methods: {
    async obtenerPokemones() {
      try {
        const respuesta = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=20');
        this.pokemones = respuesta.data.results.map((pokemon, indice) => ({
          nombre: pokemon.name,
          urlImagen: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${indice + 1}.png`,
          descubierto: false,
        }));
      } catch (error) {
        console.error('Error al obtener los pokemones:', error);
      }
    },
    onPokemonDescubierto() {
      this.contadorDescubiertos++;
    },
  },
  created() {
    this.obtenerPokemones();
  },
};
</script>

<style>
.pokemon-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
</style>