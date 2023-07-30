<script setup lang="ts">
import { ref } from 'vue'

const msg = ref('未送信')
const onFormSubmit = (): void => {
  msg.value = '送信されました'
}
</script>

<template>
  <form action="#" @submit.prevent="onFormSubmit">
    <input type="text" required />
    <button type="submit">送信</button>
  </form>
  <p>{{ msg }}</p>
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
