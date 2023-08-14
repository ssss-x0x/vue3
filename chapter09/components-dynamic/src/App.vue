<script setup lang="ts">
import { ref } from 'vue'

import InputComponent from './components/InputComponent.vue'
import RadioComponent from './components/RadioComponent.vue'
import SelectComponent from './components/SelectComponent.vue'

// 現在表示されるコンポーネントを表すテンプレート変数
const currentComponent = ref(InputComponent)
const currentComponentName = ref('InputComponent')
const currentComponent2 = ref(InputComponent)
const currentComponentName2 = ref('InputComponent')

const componentList = [
  { name: 'InputComponent', component: InputComponent },
  { name: 'RadioComponent', component: RadioComponent },
  { name: 'SelectComponent', component: SelectComponent }
]

// 現在表示させているコンポーネントに対応した配列のインデックス番号
let currentComponentIndex = 0
let currentComponentIndex2 = 0

// コンポーネントを切り替える関数
const switchComponent1 = (): void => {
  currentComponentIndex++
  if (currentComponentIndex >= componentList.length) {
    currentComponentIndex = 0
  }
  currentComponent.value = componentList[currentComponentIndex].component
  currentComponentName.value = componentList[currentComponentIndex].name
}

const switchComponent2 = (): void => {
  currentComponentIndex2++
  if (currentComponentIndex2 >= componentList.length) {
    currentComponentIndex2 = 0
  }
  currentComponent2.value = componentList[currentComponentIndex2].component
  currentComponentName2.value = componentList[currentComponentIndex2].name
}
</script>

<template>
  <section>
    <h1>KeepAliveで囲むとコンポーネントの表示切り替えをしても状態を保持しておける</h1>
    <p>コンポーネント名 : {{ currentComponentName }}</p>
    <KeepAlive>
      <component :is="currentComponent" /> </KeepAlive
    ><br />
    <button @click="switchComponent1()">切り替える</button>
  </section>
  <section>
    <h1>KeepAliveで囲まない場合、コンポーネントの表示切り替えをすると状態は初期化される</h1>
    <p>コンポーネント名 : {{ currentComponentName2 }}</p>
    <component :is="currentComponent2" /><br />
    <button @click="switchComponent2">切り替える</button>
  </section>
</template>

<style scoped>
section {
  margin: 16px;
  padding: 16px;
}
</style>
