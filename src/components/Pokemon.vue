<template>
  <div class="c-pokemon">
    <img
      class="c-pokemon__image"
      :src="getImage()"
      :alt="pokemon.name"
      :key="`${pokemon.name}-${showBack}`"
    />

    <div class="c-pokemon__info">
      <header class="c-pokemon__header">
        <h2 class="c-pokemon__name">{{ pokemon.name }}</h2>

        <label class="c-pokemon-spin" :for="`showBack-${pokemon.name}`">
          <input
            class="c-pokemon-spin__input"
            type="checkbox"
            name="showBack"
            :id="`showBack-${pokemon.name}`"
            v-model="showBack"
          />
          <RefreshCw class="c-pokemon-spin__icon" v-if="showBack" />
          <RefreshCcw class="c-pokemon-spin__icon" v-else />
        </label>
      </header>

      <p class="c-pokemon__link">More info ></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { RefreshCw, RefreshCcw } from 'lucide-vue-next'

const props = defineProps({
  pokemon: {
    type: Object,
    required: true,
  },
})

const details = ref(null)
const showBack = ref(false)

const getImage = function () {
  return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${
    showBack.value ? 'back/' : ''
  }${props.pokemon.url.split('/')[props.pokemon.url.split('/').length - 2]}.gif`
}

const getDetails = async function () {
  details.value = await fetch(props.pokemon.url).then((r) => r.json())
}

getDetails()
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

  &-spin {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    background: #111111;
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

    &__input {
      display: none;
    }
  }

  &__name {
    font-size: 1.5rem;
    font-weight: 600;
    margin: 0;

    &:first-letter {
      text-transform: uppercase;
    }
  }

  &__image {
    height: 7rem;
    width: auto;
    display: block;
    margin-bottom: -0.5rem;
  }

  &__link {
    padding: 1rem 0;
    font-size: 0.75rem;
    margin: 0 0 0 auto;
    text-decoration: underline;
  }
}

@media screen and (min-width: 480px) {
  .c-pokemon {
    width: calc((100% - 1 * 2rem) / 2);
  }
}

@media screen and (min-width: 768px) {
  .c-pokemon {
    width: calc((100% - 3 * 2rem) / 4);
  }
}
</style>
