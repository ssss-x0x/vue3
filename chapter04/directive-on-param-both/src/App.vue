<script setup lang="ts">
import { ref } from 'vue'

const pMsg = ref('ここをクリック！')
const pBgColorEvent = ref('white')
const onPClickWithEvent = (bgColor: string, event: MouseEvent): void => {
  pBgColorEvent.value = bgColor
  pMsg.value = event.timeStamp.toString()
}
</script>

<template>
  <p @click="onPClickWithEvent('green', $event)" :style="{ backgroundColor: pBgColorEvent }">
    {{ pMsg }}
  </p>

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
