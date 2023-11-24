<template>
  <div class="c-ghost" v-for="ghost in ghosts">
    <div class="c-ghost__image"></div>

    <div class="c-ghost__info">
      <header class="c-ghost__header">
        <h2 class="c-ghost__name"></h2>
        <div class="c-ghost__button"></div>
      </header>

      <p class="c-ghost__link">More info ></p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const ghosts = ref(12)
</script>

<style lang="scss">
.c-ghost {
  width: 100%;

  &__image {
    width: 7rem;
    height: 7rem;
    background: #444;
    border-radius: 2rem;
    margin-bottom: -0.5rem;
  }

  &__info {
    display: flex;
    flex-direction: column;
    background: #666;
    color: #111111;
    padding: 0.5rem 1rem;
    border-radius: 1rem 2rem 1rem 2rem;
  }

  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__name {
    width: 65%;
    height: 2.25rem;
    margin: 0;
    border-radius: 0.5rem;
    background-color: #777;
  }

  &__button {
    width: 3rem;
    height: 3rem;
    background: #777;
    border-radius: 50%;
  }

  &__link {
    padding: 1rem 0;
    color: #dfdfdf;
    font-size: 0.75rem;
    margin: 0 0 0 auto;
    text-decoration: underline;
  }
}

@media screen and (min-width: 480px) {
  .c-ghost {
    width: calc((100% - 1 * 2rem) / 2);
  }
}

@media screen and (min-width: 768px) {
  .c-ghost {
    width: calc((100% - 3 * 2rem) / 4);
  }
}
</style>
