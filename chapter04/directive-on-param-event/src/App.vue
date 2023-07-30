<script setup lang="ts">
import { ref } from 'vue'

const mousePointerX = ref(0)
const mousePointerY = ref(0)
const onImgMouseMove = (event: MouseEvent):void => {
  mousePointerX.value = event.offsetX
  mousePointerY.value = event.offsetY
}
</script>

<template>
  <section>
    <img src="./assets/logo.svg" alt="Vueのロゴ" width="200" @mousemove="onImgMouseMove">
    <p>ポインタの位置: x={{ mousePointerX }}, y={{ mousePointerY }}</p>
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
