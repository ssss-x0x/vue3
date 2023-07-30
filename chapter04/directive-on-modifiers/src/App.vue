<script setup lang="ts">
import { ref } from 'vue'

const msg = ref('まだです！')

const onEnterKey = (): void => {
  msg.value = 'エンターキーと別のキーが押下されました'
}
const onEnterKeyOnly = (): void => {
  msg.value = 'エンターキーのみが押下されました'
}
const onMetaKey = (): void => {
  msg.value = '⌘キーが押下されました'
}
const onRightButtonClick = (): void => {
  msg.value = '右クリックされました'
}
const onShiftClick = (): void => {
  msg.value = 'シフトキーを押しながらクリックされました'
}
const onMetaClick = (): void => {
  msg.value = '⌘キーを押しながらクリックされました'
}
</script>

<template>
  <p>{{ msg }}</p>
  <input
    type="text"
    placeholder="エンターキーを押下してね"
    @keydown.enter="onEnterKey"
    @keydown.enter.exact="onEnterKeyOnly"
  /><br />
  <input type="text" placeholder="⌘キーを押下してね" @keydown.meta="onMetaKey" /><br />
  <button @click.right="onRightButtonClick">右クリックしてね</button><br />
  <button @click.shift="onShiftClick">シフトキーを押しながらクリックしてね</button><br />
  <button @click.meta="onMetaClick">⌘キーを押しながらクリックしてね</button><br />
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
