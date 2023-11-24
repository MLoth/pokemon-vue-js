<template>
  <Logo />

  <div class="c-grid">
    <Loading v-if="loading" />

    <template v-else>
      <Pokemon
        v-if="pokemons"
        v-for="pokemon in pokemons"
        :pokemon="pokemon"
      ></Pokemon>
      <div v-else>
        <p>There are no pokemons</p>
      </div>
    </template>
  </div>

  <Pages @change-page="handleNewPage" />

  <!-- page x (inputfield) -->
  <!-- < x / totalPages (108) > -->
</template>

<script setup>
import { ref } from 'vue'
import Pokemon from './components/Pokemon.vue'
import Logo from './components/Logo.vue'
import Loading from './components/Loading.vue'
import Pages from './components/Pages.vue'

const pokemons = ref([])

const loading = ref(true)

// const getData = async function () {
//   const data = await fetch('https://monkey-api.be').then((response) =>
//     response.json(),
//   ).catch((error) => {
//     console.error(error)
//   })
//   monkeys.value = data
//   loading.value
// }

const getPokemons = async function (limit = 100000, page) {
  const data = await fetch(
    `https://pokeapi.co/api/v2/pokemon/?limit=${limit}&offset=${page * 12}`,
  ).then((r) => r.json())
  pokemons.value = data.results
  loading.value = false
}

const handleNewPage = function (selectedPage) {
  loading.value = true
  getPokemons(12, selectedPage)
}

getPokemons(12, 0)
</script>

<style lang="scss">
html {
  color: #fefefe;
  background: #303030;
  font-family: 'Work Sans', sans-serif;
}

.c-grid {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 2rem;
  max-width: 72rem;
  margin: 0 auto;
  padding: 2rem;
}
</style>
