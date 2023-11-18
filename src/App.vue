<template>
  <!-- Deze kan je in App.vue zetten. -->
  <Logo />

  <div class="o-grid">
    <LoadingSkeletons v-if="loading" :amount="12"></LoadingSkeletons>
    <Pokemon
      v-else
      v-for="pokemon in pokemons"
      :pokemonData="pokemon"
      :key="pokemon.name"
    >
    </Pokemon>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Logo from './components/Logo.vue'
import Pokemon from './components/Pokemon.vue'
import LoadingSkeletons from './components/LoadingSkeletons.vue'

const pokemons = ref()
const loading = ref(true)

const getPokemons = async function (limit = 12) {
  const data = await fetch(
    `https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=0`,
  ).then((r) => r.json())

  console.log(data)
  pokemons.value = data.results
  loading.value = false
}

getPokemons()
</script>

<style lang="scss">
html {
  color: #fefefe;
  background: #303030;
  font-family: 'Work Sans', sans-serif;
}

.o-grid {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 2rem;
  max-width: 72rem;
  margin: 0 auto;
  padding: 2rem;
}
</style>
