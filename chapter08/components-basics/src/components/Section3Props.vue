<script setup lang="ts">
import { ref } from 'vue'
import OneInfo from './OneInfo.vue'
import OneInfoNumber from './OneInfoNumber.vue'

// 8.3.3 親のテンプレート変数をPropsに渡す
const propsTitle = ref('発生した乱数')
const rand = calcRamdomNumber()
const propsContent = ref(rand)

function calcRamdomNumber(): number {
  return Math.round(Math.random() * 100)
}
function changeNumber(): void {
  propsContent.value = calcRamdomNumber()
}

// 8.3.4  v-forとPropsとの組み合わせ
interface Weather {
  id: number
  title: string
  content: string
}
const weatherList = ref(initWeatherList())

function initWeatherList() {
  const weatherListInit = new Map<number, Weather>()
  weatherListInit.set(1, { id: 1, title: '今日の天気', content: '今日は1日中晴れでしょう' })
  weatherListInit.set(2, { id: 2, title: '明日の天気', content: '明日は1日中雨でしょう' })
  weatherListInit.set(3, { id: 3, title: '明後日の天気', content: '明後日は1日中雪でしょう' })
  return weatherListInit
}
</script>

<template>
  <h1>8.3 Props基礎</h1>
  <section>
    <h2>8.3.2 属性に直接記述</h2>
    <OneInfo title="Propsの利用" content="子コンポーネントにデータを渡すにはPropsを利用する" />
    <h2>8.3.3 テンプレート変数を利用</h2>
    <OneInfoNumber :title="propsTitle" :content="propsContent" />
    <button @click="changeNumber">再計算</button>
    <h2>8.3.4 ループでコンポーネントを生成</h2>
    <OneInfo
      v-for="[id, weather] in weatherList"
      :key="id"
      :title="weather.title"
      :content="weather.content"
    />
  </section>
</template>

<style scoped>
section {
  border: blue 1px solid;
  margin: 16px;
  padding: 8px;
}
</style>
