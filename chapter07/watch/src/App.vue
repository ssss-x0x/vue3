<script setup lang="ts">
import { ref, watch } from 'vue'

interface Cocktail {
  id: number
  name: string
  price: number
}
// カクテル番号のテンプレート変数を用意
const cocktailNo = ref(1)

// カクテル番号に対応するカクテル情報テンプレート変数を用意
const priceMsg = ref('')

// カクテル一覧を用意
const cocktailDataListInit = new Map<number, Cocktail>()
cocktailDataListInit.set(1, { id: 1, name: 'ホワイトレディ', price: 1000 })
cocktailDataListInit.set(2, { id: 2, name: 'ブルーハワイ', price: 1500 })
cocktailDataListInit.set(3, { id: 3, name: 'ニューヨーク', price: 1100 })
cocktailDataListInit.set(4, { id: 4, name: 'マティーニ', price: 1500 })
cocktailDataListInit.set(5, { id: 5, name: 'モヒート', price: 800 })

watch(
  cocktailNo,
  (): void => {
    priceMsg.value = getCocktailInfo(cocktailNo.value)
  },
  { immediate: true }
)

function getCocktailInfo(cocktailNo: number): string {
  const cocktail = cocktailDataListInit.get(cocktailNo)
  let msg = '該当カクテルはありません。'

  if (cocktail !== undefined) {
    msg = `該当するカクテルは${cocktail.name}で、 価格は${cocktail.price}です。`
  }
  return msg
}

// cocktailNoを1秒ごとに乱数を使って変更
const length = cocktailDataListInit.size
setInterval((): void => {
  cocktailNo.value = Math.round(Math.random() * (length - 1)) + 1
}, 1000)
</script>

<template>
  <p>現在のカクテル番号: {{ cocktailNo }}</p>
  <p>{{ priceMsg }}</p>
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
