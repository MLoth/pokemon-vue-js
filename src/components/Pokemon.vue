<template>
  <div class="c-pokemon">
    <img
      :src="getPokemonImageUrl()"
      :alt="`Avatar van ${pokemonData.name}`"
      class="c-pokemon__image"
    />

    <div class="c-pokemon__info">
      <header class="c-pokemon__header">
        <h2 class="c-pokemon__name">{{ pokemonData.name }}</h2>

        <label class="c-pokemon-spin" for="">
          <input class="c-pokemon-spin__input" type="checkbox" name="" id="" />

          <RotateCw class="c-pokemon-spin__icon" />
          <RotateCcw class="c-pokemon-spin__icon" />
        </label>
      </header>

      <p class="c-pokemon__info">More info <ChevronRight /></p>
    </div>
  </div>
</template>

<!-- Nu moeten we die data hier nog opvangen! -->
<script setup>
import { RotateCcw, RotateCw, ChevronRight } from 'lucide-vue-next'

const props = defineProps({
  pokemonData: {
    type: Object, // { }
    required: true,
  },
})

const getPokemonId = function () {
  const partsOfUrl = props.pokemonData.url.split('/')
  const pokemonId = partsOfUrl[partsOfUrl.length - 2]
  return pokemonId
}

const getPokemonImageUrl = function () {
  return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${getPokemonId()}.gif`
}
</script>
