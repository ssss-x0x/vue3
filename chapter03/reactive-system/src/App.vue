<script setup lang="ts">
import { ref } from 'vue'

const options = { hour: 'numeric', minute:'numeric', second:'numeric' }
const now = new Date()
const nowStr = now.toLocaleDateString(undefined, options)
let timeStr = nowStr
const timeStrRef = ref(nowStr)

// リアクティブになっていない変数を更新
function changeTime(): void {
  const newTime = new Date()
  const newTimeStr = newTime.toLocaleDateString(undefined, options)
  timeStr = newTimeStr
}

// refでリアクティブなデータとなっている変数を更新
function changeTimeRef(): void {
  const newTime = new Date()
  const newTimeStr = newTime.toLocaleDateString(undefined, options)
  timeStrRef.value = newTimeStr
}

setInterval(changeTime, 1000)
setInterval(changeTimeRef, 5000)
</script>

<template>
  <p>現在時刻: {{ timeStr }}</p>
  <p>現在時刻(ref): {{ timeStrRef }}</p>
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
