<script setup lang="ts">
import { ref } from 'vue'

// 6.2.3 Mapのループ
const cocktailListInit = new Map<number, string>()
cocktailListInit.set(2345, 'ホワイトレディ')
cocktailListInit.set(4412, 'ブルーハワイ')
cocktailListInit.set(6792, 'ニューヨーク')
cocktailListInit.set(7021, 'キューバリブレ')
cocktailListInit.set(9682, 'マリブオレンジ')

const cocktailList = ref(cocktailListInit)

// 6.2.4 オブジェクトのループ
const whiteLadyInit: {
  id: number
  name: string
  price: number
  recipe: string
} = {
  id: 2345,
  name: 'ホワイトレディ',
  price: 1200,
  recipe: 'ジン30ml + コワントロー15ml + レモン果汁15ml'
}

const whiteLady = ref(whiteLadyInit)

// 6.2.5 オブジェクトの配列のループ
interface Cocktail {
  id: number
  name: string
  price: number
}

const cocktailDataListInit: Cocktail[] = [
  { id: 2345, name: 'ホワイトレディ', price: 1200 },
  { id: 4412, name: 'ブルーハワイ', price: 1500 },
  { id: 6792, name: 'ニューヨーク', price: 1100 },
  { id: 8429, name: 'マティーニ', price: 1500 }
]

const cocktailDataList = ref(cocktailDataListInit)

// 6.2.6 Mapとオブジェクトの組み合わせのループ
const cocktailDataListInit2 = new Map<number, Cocktail>()
cocktailDataListInit2.set(2345, { id: 2345, name: 'ホワイトレディ', price: 1200 })
cocktailDataListInit2.set(4412, { id: 4412, name: 'ブルーハワイ', price: 1500 })
cocktailDataListInit2.set(6792, { id: 6792, name: 'ニューヨーク', price: 1100 })
cocktailDataListInit2.set(8429, { id: 8429, name: 'マティーニ', price: 1500 })

const cocktailDataList2 = ref(cocktailDataListInit2)

// 6.2.7 カウンタ変数を利用したループ
</script>

<template>
  <section>
    <h2>6.2.3 Mapのループ</h2>
    <ul>
      <li v-for="[id, cocktailName] in cocktailList" :key="id">
        IDが{{ id }}のカクテルは{{ cocktailName }}
      </li>
    </ul>
  </section>

  <section>
    <h2>6.2.4 オブジェクトのループ</h2>
    <dl>
      <template v-for="(value, key) in whiteLady" :key="key">
        <dt>{{ key }}</dt>
        <dd>{{ value }}</dd></template
      >
    </dl>
  </section>

  <section>
    <h2>6.2.5 オブジェクトの配列のループ</h2>
    <ul>
      <li v-for="cocktailItem in cocktailDataList" :key="cocktailItem.id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </section>

  <section>
    <h2>6.2.6 Mapとオブジェクトの組み合わせのループ</h2>
    <ul>
      <li v-for="[id, cocktailItem] in cocktailDataList2" :key="id">
        {{ cocktailItem.name }}の値段は {{ cocktailItem.price }}
      </li>
    </ul>
  </section>

  <section>
    <h2>6.2.7 カウンタ変数を利用したループ</h2>
    <ul>
      <li v-for="r in 5" :key="r">半径{{ r }} の円周: {{ 2 * r * 3.14 }}</li>
    </ul>
  </section>
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
