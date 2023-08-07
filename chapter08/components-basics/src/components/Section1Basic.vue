<script setup lang="ts">
import OneSection from './OneSection.vue'
</script>

<template>
  <h1>8.1 コンポーネント基礎</h1>
  <section>
    <h2>コンポーネント1個</h2>
    <OneSection />
  </section>
  <section>
    <h2>コンポーネントが複数</h2>
    <OneSection />
    <OneSection />
    <OneSection />
  </section>
</template>

<style scoped>
section {
  border: blue 1px solid;
  margin: 16px;
  padding: 8px;
}
</style>
