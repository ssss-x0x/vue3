<script setup lang="ts">
import { ref } from 'vue'

const randValue = ref('not yet')

const onButtonClick = (): void => {
  const rand = Math.round(Math.random() * 10)
  randValue.value = String(rand)
}

let followers = ref('😃')
const addFollower = (): void => {
  followers.value += '😃'
}
</script>

<template>
  <section>
    <button @click="onButtonClick">クリック！</button>
    <p>クリックの結果: {{ randValue }}</p>
    <hr />

    <p>打鍵の数だけ顔が増えるよ</p>
    <p>{{ followers }}</p>
    <input type="text" @kewdown="addFollower" />
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
