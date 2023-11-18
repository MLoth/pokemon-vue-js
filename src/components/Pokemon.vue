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

        <label class="c-pokemon-spin" :for="pokemonData.name">
          <input
            class="c-pokemon-spin__input sr-only"
            type="checkbox"
            :id="pokemonData.name"
            v-model="showBack"
          />

          <span class="sr-only"
            >Toggle Pokemon from back to front and vice versa.</span
          >

          <RefreshCcw v-if="showBack" class="c-pokemon-spin__icon" />
          <RefreshCw v-else class="c-pokemon-spin__icon" />
        </label>
      </header>

      <p class="c-pokemon__link">More info <ChevronRight /></p>
    </div>
  </div>
</template>

<!-- Nu moeten we die data hier nog opvangen! -->
<script setup>
import { ref } from 'vue'
import { RefreshCcw, RefreshCw, ChevronRight } from 'lucide-vue-next'

const props = defineProps({
  pokemonData: {
    type: Object, // { }
    required: true,
  },
})

const showBack = ref(false)
// TODO: voorzie een goede focus state bij de checkbox - tip: scss
// TODO: verberg de originele checkbox - tip: kan beter...

const getPokemonId = function () {
  const partsOfUrl = props.pokemonData.url.split('/')
  const pokemonId = partsOfUrl[partsOfUrl.length - 2]
  return pokemonId
}

const getPokemonImageUrl = function () {
  const baseUrl = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated`

  if (showBack.value) return `${baseUrl}/back/${getPokemonId()}.gif`
  return `${baseUrl}/${getPokemonId()}.gif`
}
</script>

<style lang="scss">
.c-pokemon {
  width: 100%;

  &__info {
    display: flex;
    flex-direction: column;
    background: #444;
    color: #fff;
    padding: 0.5rem 1rem;
    border-radius: 1rem 2rem 1rem 2rem;
  }

  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__name {
    font-size: 1.5rem;
    font-weight: 600;
    margin: 0;

    &:first-letter {
      text-transform: uppercase;
    }
  }

  &-spin {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    background: #111;
    border-radius: 50%;
    height: 3rem;
    width: 3rem;
    cursor: pointer;
    margin-left: 1rem;
    transition: background 0.2s ease-in-out;
    color: white;

    &:hover {
      background: #808080;
    }

    // Als er focus is in de label!
    &:focus-within {
      outline: 3px solid lightcyan;
    }
  }

  &__image {
    height: 7rem; // UITZONDERLIJK! Een (vaste) hoogte die groter is dan de image
    width: auto;
    display: block;
    margin-bottom: -0.5rem;
  }

  &__link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 1rem 0;
    font-size: 0.75rem;
    margin: 0 0 0 auto; // push to the right
    text-decoration: underline;
  }
}

.sr-only {
  // sr-only = screenreader only
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}

// TODO: maak de pokemons:
// vanaf 480px in 2 kolommen
@media screen and (min-width: 480px) {
  .c-pokemon {
    // Tussen de pokemons 1 x 2rem ruimte
    width: calc((100% - 1 * 2rem) / 2);
  }
}

// vanaf 768px in 4 kolommen
@media screen and (min-width: 768px) {
  .c-pokemon {
    // Tussen de pokemons 3 x 2rem ruimte
    // Uiteindelijk 4 kolommen -> /4
    width: calc((100% - 3 * 2rem) / 4);
  }
}
</style>
