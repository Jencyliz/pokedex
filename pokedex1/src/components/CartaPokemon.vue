<template>
    <div class="carta-pokemon">
      <img 
        :src="pokemon.urlImagen" 
        :class="{ desenfocado: !pokemon.descubierto }"
        alt="pokemon" 
      />
      <div v-if="!pokemon.descubierto">
        <input v-model="adivinanzaUsuario" @keyup.enter="comprobarPokemon" placeholder="Escribe el nombre" />
        <button @click="comprobarPokemon">Descubrir</button>
      </div>
      <p v-else>{{ pokemon.nombre }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: ['pokemon'],
    data() {
      return {
        adivinanzaUsuario: '',
      };
    },
    methods: {
      comprobarPokemon() {
        if (this.adivinanzaUsuario.toLowerCase() === this.pokemon.nombre.toLowerCase()) {
          this.pokemon.descubierto = true;
          this.$emit('pokemon-descubierto');
        } else {
          alert('Nombre incorrecto');
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .carta-pokemon {
    text-align: center;
    margin: 10px;
  }
  .desenfocado {
    filter: blur(10px);
  }
  </style>  