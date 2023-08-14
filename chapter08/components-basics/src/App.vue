<script setup lang="ts">
import Section1Basic from './components/Section1Basic.vue'
import Section2WithModel from './components/Section2WithModel.vue'
import Section3Props from './components/Section3Props.vue'
import Section4Advanced from './components/Section4Advanced.vue'
import Section5Emit from './components/Section5Emit.vue'
</script>

<template>
  <section>
    <Section1Basic />
  </section>
  <section>
    <Section2WithModel />
  </section>
  <section>
    <Section3Props />
  </section>
  <section>
    <Section4Advanced />
  </section>
  <section>
    <Section5Emit />
  </section>
</template>

<style scoped>
section {
  padding: 8px;
}
</style>
