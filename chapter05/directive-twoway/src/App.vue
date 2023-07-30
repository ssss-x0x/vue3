<script setup lang="ts">
import { ref } from 'vue'

const inputName2Way = ref('双方向')
const oninputName2Way = (event: Event): void => {
  const element = event.target as HTMLInputElement
  inputName2Way.value = element.value
}
</script>

<template>
  <section>
    <input type="text" :value="inputName2Way" @input="oninputName2Way" />
    <p>{{ inputName2Way }}</p>
  </section>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
