<script setup lang="ts">
import WithModel from './WithModel.vue'
</script>

<template>
  <h1>8.2 コンポーネントの独立性</h1>
  <section>
    <h2>v-modelを含むコンポーネント</h2>
    <WithModel />
    <WithModel />
  </section>
</template>

<style scoped>
section {
  border: purple 1px solid;
  margin: 16px;
  padding: 8px;
}
</style>
