<script setup lang="ts">
import { ref } from 'vue'

// Propsインターフェースの定義
interface Props {
  id: number
  name: string
  email: string
  points: number
  note?: string
}

const props = withDefaults(defineProps<Props>(), { note: '-' })

const localPoint = ref(props.points)

const pointUp = (): void => {
  localPoint.value++
}
</script>

<template>
  <section class="box">
    <h4>{{ name }}さんの情報</h4>
    <dl>
      <dt>ID</dt>
      <dd>{{ id }}</dd>
      <dt>メールアドレス</dt>
      <dd>{{ email }}</dd>
      <dt>保有ポイント</dt>
      <dd>{{ localPoint }}</dd>
      <dt>備考</dt>
      <dd>{{ note }}</dd>
    </dl>
    <button @click="pointUp">ポイント加算</button>
  </section>
</template>

<style scoped>
section.box {
  border: pink 1px solid;
  margin: 16px;
  padding: 16px;
}
</style>
