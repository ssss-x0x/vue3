<script setup lang="ts">
import { ref, computed } from 'vue'

// 6.1.1 条件分岐ディレクティブの基本 v-if
const number = ref(80)
const showOrNot = computed((): boolean => {
  const rand = Math.round(Math.random() * 100)

  return rand >= 50
})

// 6.1.2 条件分岐ディレクティブをフルセットで利用した場合
// 6.1.3 ディレクティブ記述のためのタグ template
const randomNumber = computed((): number => {
  return Math.round(Math.random() * 100)
})
</script>

<template>
  <section>
    <h2>6.1.1 条件分岐ディレクティブの基本 v-if</h2>
    <p v-if="number >= 50">条件に合致したので表示①</p>
    <p v-if="Math.round(Math.random() * 100) >= 50">条件に合致したので表示②</p>
    <p v-if="showOrNot">条件に合致したので表示③</p>
  </section>

  <section>
    <h2>6.1.2 条件分岐ディレクティブをフルセットで利用した場合</h2>
    <p>
      点数は{{ randomNumber }}点で、
      <span v-if="randomNumber >= 80">優です。</span>
      <span v-else-if="randomNumber >= 70">良です。</span>
      <span v-else-if="randomNumber >= 60">可です。</span>
      <span v-else>不可です。</span>
    </p>
  </section>

  <section>
    <h2>6.1.3 ディレクティブ記述のためのタグ template</h2>
    <p>
      点数は{{ randomNumber }}点で、
      <template v-if="randomNumber >= 80"
        >優です。<span style="color: red">すばらしい！</span></template
      >
      <template v-else-if="randomNumber >= 70">良です。</template>
      <template v-else-if="randomNumber >= 60">可です。</template>
      <template v-else>不可です。</template>
    </p>
  </section>

  <section>
    <h2>6.1.4 v-ifと似て非なる v-show</h2>
    <section>
      v-ifを利用
      <p v-if="showOrNot">条件に合致したので表示</p>
    </section>
    <section>
      v-showを利用
      <p v-show="showOrNot">条件に合致したので表示</p>
    </section>
  </section>
</template>

<style scoped></style>
