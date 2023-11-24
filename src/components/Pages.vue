<template>
  <div class="c-pages">
    <button
      class="c-pages__action"
      @click="changePage(-1)"
      :disabled="currentPage === 0"
    >
      <ChevronLeft class="c-pages__icon" />
    </button>

    <p class="c-pages__current">{{ currentPage + 1 }}</p>

    <p class="c-pages__divider">/</p>

    <p class="c-pages__total">108</p>

    <button
      class="c-pages__action"
      @click="changePage(+1)"
      :disabled="currentPage === 107"
    >
      <ChevronRight class="c-pages__icon" />
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { ChevronLeft, ChevronRight } from 'lucide-vue-next'

const emit = defineEmits(['changePage'])

const currentPage = ref(0)

const changePage = function (by) {
  if (currentPage.value === 0 && by === -1) return
  if (currentPage.value === 107 && by === 1) return

  currentPage.value = currentPage.value + by
  emit('changePage', currentPage.value)
}
</script>

<style lang="scss">
.c-pages {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem 0;
  gap: 1rem;

  &__action {
    background: #444;
    border-radius: 50%;
    width: 3rem;
    height: 3rem;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;

    &:hover {
      background: #666;
    }

    &:focus-visible {
      outline: 2px solid #fff;
    }

    &:disabled {
      pointer-events: none;
      background: #111;
      color: #333;
    }
  }

  &__icon {
    stroke: currentColor;
  }

  &__current {
  }

  &__divider {
  }

  &__total {
  }
}
</style>
