<template>
  <!-- Deze kan je in App.vue zetten. -->
  <Logo />

  <Pokemon
    v-for="pokemon in pokemons"
    :pokemonData="pokemon"
    :key="pokemon.name"
  >
  </Pokemon>
</template>

<script setup>
import { ref } from 'vue'
import Logo from './components/Logo.vue'
import Pokemon from './components/Pokemon.vue'

const pokemons = ref()

const getPokemons = async function (limit = 12) {
  const data = await fetch(
    `https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=0`,
  ).then((r) => r.json())

  console.log(data)
  pokemons.value = data.results
}

getPokemons()
</script>

<style lang="scss">
html {
  color: #fefefe;
  background: #303030;
  font-family: 'Work Sans', sans-serif;
}
</style>
