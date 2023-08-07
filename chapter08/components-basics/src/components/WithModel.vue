<script setup lang="ts">
import { ref } from 'vue'

const name = ref('名無し')
</script>

<template>
  <section class="section-model">
    <p>{{ name }}さんですね！</p>
    <input type="text" v-model="name" />
  </section>
</template>

<style scoped>
section.section-model {
  border: orange 1px dashed;
  margin: 16px;
  padding: 8px;
}
</style>
