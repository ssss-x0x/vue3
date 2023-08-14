<script setup lang="ts">
import { ref } from 'vue'
interface Props {
  name: string
}

defineProps<Props>()
</script>
<template>
  <section class="box">
    <h1>{{ name }}さんの状況</h1>
    <slot><p>問題ありません。</p></slot>
    <h4>詳細内容</h4>
    <slot name="detail">
      <p>特にありません。</p>
    </slot>
  </section>
</template>

<style scoped>
.box {
  border: lightgreen 1px solid;
  margin: 16px;
  padding: 16px;
}
</style>
