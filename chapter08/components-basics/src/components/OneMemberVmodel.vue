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
  (event: 'update:points', points: number): void
}

const props = defineProps<Props>()
const emit = defineEmits<Emits>()

const localNote = computed((): string => {
  return props.note !== undefined ? props.note : '--'
})

const onInput = (event: Event): void => {
  const element = event.target as HTMLInputElement
  const inputPoints = Number(element.value)
  emit('update:points', inputPoints)
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
      <dd><input type="number" :value="points" @input="onInput" /></dd>
      <dt>備考</dt>
      <dd>{{ localNote }}</dd>
    </dl>
  </section>
</template>

<style scoped>
section.box {
  border: pink 1px solid;
  margin: 16px;
  padding: 16px;
}
</style>
