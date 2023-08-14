<script setup lang="ts">
interface Props {
  rand: number
}

interface Emits {
  (event: 'createNewRand'): void
}

defineProps<Props>()
const emit = defineEmits<Emits>()

const onNewRandButtonClick = (): void => {
  emit('createNewRand')
}
</script>

<template>
  <section class="box">
    <p>子コンポーネントで乱数を表示 {{ rand }}</p>
    <button @click="onNewRandButtonClick">新たな乱数を生成する</button>
  </section>
</template>

<style scoped>
.box {
  border: green 1px dashed;
  margin: 10px;
}
</style>
