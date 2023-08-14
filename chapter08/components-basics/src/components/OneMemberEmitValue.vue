<script setup lang="ts">
import { computed } from 'vue'

// Propsインターフェースの定義
interface Props {
  id: number
  name: string
  email: string
  points: number
  note?: string
}

interface Emits {
  (event: 'incrementPoint', id: number): void
}

const props = defineProps<Props>()
const emit = defineEmits<Emits>()

const localNote = computed((): string => {
  return props.note !== undefined ? props.note : '--'
})

const pointUp = (): void => {
  emit('incrementPoint', props.id)
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
      <dd>{{ points }}</dd>
      <dt>備考</dt>
      <dd>{{ localNote }}</dd>
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
