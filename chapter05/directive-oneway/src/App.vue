<script setup lang="ts">
import { ref } from 'vue'

const inputNameBind = ref('しんちゃん')
const inputNameOn = ref('ななし')
const onInputName = (event: Event): void => {
  const element = event.target as HTMLInputElement
  inputNameOn.value = element.value
}
</script>

<template>
  <section>
    <input type="text" :value="inputNameBind" />
    {{ inputNameBind }}
  </section>
  <br />
  <section>
    <input type="text" @input="onInputName" />
    <p>{{ inputNameOn }}</p>
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
