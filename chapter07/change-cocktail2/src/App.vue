<script lang="ts">
import { defineComponent, ref, computed } from 'vue'

interface Cocktail {
  id: number
  name: string
  price: number
}
export default defineComponent({
  name: 'App',
  setup() {
    // カクテル一覧を用意
    const cocktailDataListInit = setCocktailDataList()

    // カクテル番号のテンプレート変数を用意
    const cocktailNo = ref(1)

    // カクテル番号に他対応するカクテル情報の算出プロパティを用意
    const priceMsg = computed((): string => {
      const cocktail = cocktailDataListInit.get(cocktailNo.value)
      let msg = '該当カクテルはありません。'

      if (cocktail !== undefined) {
        msg = `該当するカクテルは${cocktail.name}で、 価格は${cocktail.price}です。`
      }
      return msg
    })
    // cocktailNoを1秒ごとに乱数を使って変更
    const length = cocktailDataListInit.size
    setInterval((): void => {
      cocktailNo.value = Math.round(Math.random() * (length - 1)) + 1
    }, 1000)

    return {
      cocktailNo,
      priceMsg
    }
  }
})

function setCocktailDataList() {
  const cocktailDataListInit = new Map<number, Cocktail>()
  cocktailDataListInit.set(1, { id: 1, name: 'ホワイトレディ', price: 1000 })
  cocktailDataListInit.set(2, { id: 2, name: 'ブルーハワイ', price: 1500 })
  cocktailDataListInit.set(3, { id: 3, name: 'ニューヨーク', price: 1100 })
  cocktailDataListInit.set(4, { id: 4, name: 'キューバリブレ', price: 1500 })
  cocktailDataListInit.set(5, { id: 5, name: 'モヒート', price: 800 })

  return cocktailDataListInit
}
</script>

<template>
  <p>現在のカクテル番号: {{ cocktailNo }}</p>
  <p>{{ priceMsg }}</p>
</template>

<style scoped></style>
