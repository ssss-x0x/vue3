<script setup lang="ts">
import { ref, computed } from 'vue'

// 6.3.1 ループ対象データの絞り込み
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
const cocktail1500 = computed((): Cocktail[] => {
  const newList = cocktailDataList.value.filter((cocktailItem: Cocktail): boolean => {
    return cocktailItem.price === 1500
  })
  return newList
})

// 6.3.2 配列のデータ操作
const cocktailDataListInit2: string[] = [
  'ホワイトレディ',
  'ブルーハワイ',
  'ニューヨーク',
  'マティーニ'
]
const cocktailList2 = ref(cocktailDataListInit2)
const changeCocktailList = (): void => {
  cocktailList2.value = ['バラライカ', 'XYZ', 'マンハッタン']
}
const addCocktailList = (): void => {
  cocktailList2.value.push('ブルームーン')
}
const deleteFromCocktailList = (): void => {
  cocktailList2.value.pop()
}

// 6.3.3 Mapのデータ操作
const cocktailListInitMap = new Map<number, string>()
cocktailListInitMap.set(2345, 'ホワイトレディ')
cocktailListInitMap.set(4412, 'ブルーハワイ')
cocktailListInitMap.set(6792, 'ニューヨーク')
cocktailListInitMap.set(7021, 'キューバリブレ')
cocktailListInitMap.set(9682, 'マリブオレンジ')

const cocktailListMap = ref(cocktailListInitMap)
const changeCocktailListMap = (): void => {
  cocktailListMap.value.clear()
  cocktailListMap.value.set(3416, 'バラライカ')
  cocktailListMap.value.set(5517, 'XYZ')
  cocktailListMap.value.set(7415, 'マンハッタン')
}
const addCocktailListMap = (): void => {
  cocktailListMap.value.set(8894, 'ブルームーン')
}
const deleteFromCocktailListMap = (): void => {
  cocktailListMap.value.delete(5517)
}

// 6.3.4 オブジェクト内のデータ変更
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
const changeWhiteLadyPrice = (): void => {
  whiteLady.value.price = 1500
}

// 6.3.5 リストデータ内のオブジェクトの変更
const cocktailDataListInitMapObject = new Map<number, Cocktail>()
cocktailDataListInitMapObject.set(2345, { id: 2345, name: 'ホワイトレディ', price: 1200 })
cocktailDataListInitMapObject.set(4412, { id: 4412, name: 'ブルーハワイ', price: 1500 })
cocktailDataListInitMapObject.set(6792, { id: 6792, name: 'ニューヨーク', price: 1100 })
cocktailDataListInitMapObject.set(8429, { id: 8429, name: 'マティーニ', price: 1500 })

const cocktailDataListMapObject = ref(cocktailDataListInitMapObject)

const cocktailPrice1500 = computed((): Map<number, Cocktail> => {
  const newList = new Map<number, Cocktail>()
  cocktailDataListMapObject.value.forEach((value: Cocktail, key: number): void => {
    if (value.price === 1500) {
      newList.set(key, value)
    }
  })
  return newList
})

const changeWhiteLadyPriceInList = (): void => {
  const whiteLady = cocktailDataListMapObject.value.get(2345) as Cocktail // undefinedである可能性エラーを避けるために強制的にCocktailへ型変換している＝型アサーション
  whiteLady.price = 1500

  /**
   * id 2345が存在するか確実ではない場合は、型アサーションを使わずに存在チェックを行う
   */
  //  const whiteLady2 = cocktailDataListMapObject.value.get(2345)
  //  if(whiteLady2) {
  //   whiteLady2.price = 1500
  //  }
}
</script>

<template>
  <section>
    <h2>6.3.1 ループ対象データの絞り込み</h2>
    <h3>全てのカクテルリスト</h3>
    <ul>
      <li v-for="cocktailItem in cocktailDataList" :key="cocktailItem.id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
    <h3>値段が1500円のカクテルリスト</h3>
    <ul>
      <li v-for="cocktailItem in cocktail1500" :key="'cocktail1500' + cocktailItem.id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </section>

  <section>
    <h2>6.3.2 配列のデータ操作</h2>
    <ul>
      <li v-for="(cocktailName, index) in cocktailList2" :key="cocktailName">
        {{ cocktailName }}（インデックス{{ index }}）
      </li>
    </ul>
    <p>cocktailList2を<button @click="changeCocktailList">変更</button></p>
    <p>cocktailList2の末尾に「ブルームーン」を<button @click="addCocktailList">追加</button></p>
    <p>cocktailList2から末尾の要素を<button @click="deleteFromCocktailList">削除</button></p>
  </section>

  <section>
    <h2>6.3.3 Mapのデータ操作</h2>
    <ul>
      <li v-for="[id, cocktailName] in cocktailListMap" :key="id">
        IDが{{ id }}のカクテルは{{ cocktailName }}
      </li>
    </ul>
    <p>cocktailListMapを<button @click="changeCocktailListMap">変更</button></p>
    <p>
      cocktailListMapの末尾に「ブルームーン」を<button @click="addCocktailListMap">追加</button>
    </p>
    <p>cocktailListMapから5517のXYZを<button @click="deleteFromCocktailListMap">削除</button></p>
  </section>

  <section>
    <h2>6.3.4 オブジェクト内のデータ変更</h2>
    <dl>
      <template v-for="(value, key) in whiteLady" :key="key">
        <dt>{{ key }}</dt>
        <dd>{{ value }}</dd>
      </template>
    </dl>
    <p>価格を1500円に<button @click="changeWhiteLadyPrice">変更</button></p>
  </section>

  <section>
    <h2>6.3.5 リストデータ内のオブジェクトの変更</h2>
    <h3>全てのカクテルリスト</h3>
    <ul>
      <li v-for="[id, cocktailItem] in cocktailDataListMapObject" :key="id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
    <h3>値段が1500円のカクテルリスト</h3>
    <ul>
      <li v-for="[id, cocktailItem] in cocktailPrice1500" :key="'cocktailPrice1500' + id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
    <p>
      cocktailDataListMapObject内のホワイトレディの価格を1500円に
      <button @click="changeWhiteLadyPriceInList">変更</button>
    </p>
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
