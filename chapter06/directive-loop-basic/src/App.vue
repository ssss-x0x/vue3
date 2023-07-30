<script setup lang="ts">
import { ref } from 'vue'

// 6.2.1
const cocktailListInit: string[] = ['ホワイトレディ', 'ブルーハワイ', 'ニューヨーク']
const cocktailList = ref(cocktailListInit) // データの用意とリアクティブ化を分離しているため可読性が上がる

// 6.2.2
const cocktailListInit2: { [key: number]: string } = {
  2345: 'ホワイトレディ',
  4412: 'ブルーハワイ',
  6792: 'ニューヨーク',
  5962: 'キューバリブレ'
}
const cocktailList2 = ref(cocktailListInit2)
</script>

<template>
  <section>
    <h2>6.2.1 ループのディレクティブである v-for</h2>
    <ul>
      <li v-for="cocktailName in cocktailList" :key="cocktailName">{{ cocktailName }}</li>
    </ul>

    <ul>
      <li v-for="(cocktailName, index) in cocktailList" :key="cocktailName">
        {{ cocktailName }}(インデックス: {{ index }})
      </li>
    </ul>
  </section>

  <section>
    <h2>6.2.2 連想配列のループ</h2>
    <ul>
      <li v-for="(cocktail, id) in cocktailList2" :key="id">
        IDが{{ id }}のカクテルは{{ cocktail }}
      </li>
    </ul>
    <br />
    <ul>
      <li v-for="(cocktail, id, index) in cocktailList2" :key="'cocktailListWithIdx' + id">
        {{ index + 1 }} : IDが{{ id }}のカクテルは{{ cocktail }}
      </li>
    </ul>
  </section>
</template>

<style scoped></style>
