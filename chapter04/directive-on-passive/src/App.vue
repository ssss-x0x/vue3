<script setup lang="ts">
import { ref } from 'vue'

const mousePointerX = ref(0)
const mousePointerY = ref(0)
const onScroll = (event: UIEvent): void => {
  console.log(event)
  // mousePointerX.value = event.offsetX
  // mousePointerY.value = event.offsetY
}
</script>

<template>
  <div class="longHeight" @scroll.passive="onScroll">
    <p>x: {{ mousePointerX }}</p>
    <p>y: {{ mousePointerY }}</p>
  </div>
</template>

<style scoped>
.longHeight {
  background-color: #eee;
  height: 2000px;
}
</style>
