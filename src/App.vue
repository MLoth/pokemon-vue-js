<template>
  <h1>Pokemon!</h1>
</template>

<script setup>
const getPokemons = async function (limit = 12) {
  const data = await fetch(
    `https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=0`,
  ).then((r) => r.json())

  console.log(data)
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
