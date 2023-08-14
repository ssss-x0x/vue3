<script setup lang="ts">
import { reactive } from 'vue'

const memberInfo = reactive({
  name: '田中太郎',
  state: '問題ありません。',
  note: '特にありません。'
})

const locationInfo = reactive({
  place: '東京',
  date: '2021/10/10',
  time: '10:00'
})
</script>

<template>
  <section class="box">
    <slot :member="memberInfo" :location="locationInfo">
      <h1>{{ memberInfo.name }}さんの状況</h1>
      <p>{{ memberInfo.state }}</p>
      <h2>ロケーション情報</h2>
      <p>{{ locationInfo.place }}, {{ locationInfo.date }} {{ locationInfo.time }}</p>
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
