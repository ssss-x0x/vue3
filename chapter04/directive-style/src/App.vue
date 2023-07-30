<script setup lang="ts">
import { ref, computed } from 'vue'

const msg = ref('こんにちは世界')
const msg_text_red = ref('red')
const msg_text_color = ref('white')
const msg_bg_color = ref('black')
const msg_styles = ref({
  color: 'white',
  backgroundColor: 'black'
})
const msg_styles_2 = ref({
  fontSize: '24pt'
})
const msg_styles_3 = ref({
  color: 'pink',
  fontSize: '24pt'
})
const text_size = computed((): string => {
  const size = Math.round(Math.random() * 25) + 10
  return `${size}pt`
})
</script>

<template>
  <p :style="{ color: msg_text_red }">{{ msg }}</p>
  <p :style="{ color: 'pink' }">{{ msg }}</p>
  <p :style="{ fontSize: text_size }">{{ msg }}</p>
  <p :style="{ 'font-size': text_size, color: 'blue' }">{{ msg }}</p>
  <p :style="{ color: msg_text_color, backgroundColor: msg_bg_color }">{{ msg }}</p>
  <p :style="{ color: msg_text_color, 'background-color': msg_bg_color }">{{ msg }}</p>
  <p :style="msg_styles">{{ msg }}</p>
  <p :style="[msg_styles, msg_styles_2]">{{ msg }}</p>
  <p :style="[msg_styles, msg_styles_3]">{{ msg }}</p>
  <p :style="[msg_styles_3, msg_styles]">{{ msg }}</p>
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
