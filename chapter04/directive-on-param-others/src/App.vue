<script setup lang="ts">
import { ref } from 'vue'

type allowColors = 'red' | 'pink' | 'blue' | 'white'

const pBgColor = ref('white')
const onPClick = (bgColor: allowColors): void => {
  pBgColor.value = bgColor
}

</script>

<template>
  <p :style="{ backgroundColor: pBgColor }">
    ボタンをクリックすると背景色が変わります
  </p>
  <button @click="onPClick('red')">赤</button>
  <button @click="onPClick('pink')">ピンク</button>
  <button @click="onPClick('blue')">青</button>
  <button @click="onPClick('white')">白</button>
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
