<template>
  <div v-for="skeleton in amount" class="c-skeleton">
    <div class="c-skeleton__image"></div>

    <div class="c-skeleton__info">
      <div class="c-skeleton__header">
        <div class="c-skeleton__name"></div>
        <div class="c-skeleton__button"></div>
      </div>

      <p class="c-skeleton__link">More info <ChevronRight /></p>
    </div>
  </div>
</template>

<script setup>
import { ChevronRight } from 'lucide-vue-next'

// TODO: We willen niet 1 zien, maar x aantal die we doorgeven als prop
defineProps({
  amount: {
    type: Number,
    default: 4,
  },
})
// TODO: zet hier een prop op die een getal doorgeeft
</script>

<style lang="scss">
// https://pastebin.com/2XRmW8Zm
.c-skeleton {
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
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 1rem 0;
    color: #dfdfdf;
    font-size: 0.75rem;
    margin: 0 0 0 auto;
    text-decoration: underline;
  }
}

@media screen and (min-width: 480px) {
  .c-skeleton {
    width: calc((100% - 1 * 2rem) / 2);
  }
}

@media screen and (min-width: 768px) {
  .c-skeleton {
    width: calc((100% - 3 * 2rem) / 4);
  }
}
</style>
