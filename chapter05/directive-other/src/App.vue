<script setup lang="ts">
import { ref } from 'vue'

const htmlStr = ref('<a href="https://vuejs.org" target="_blank">Vue.jsのページ</a>')

const price = ref(1000)

const hello = ref('こんにちは！')
</script>

<template>
  <section>
    <h2>HTML文字列をそのまま出力する v-html</h2>
    <section>{{ htmlStr }}</section>
    <section v-html="htmlStr"></section>
  </section>

  <br />

  <section>
    <h2>静的コンテンツとして表示させる v-pre</h2>
    <section v-pre>
      <p v-on:click="showHello">{{ hello! }}</p>
    </section>
  </section>

  <br />

  <section>
    <h2>データバインドを一度だけ行う v-once</h2>
    <section>
      <input type="number" v-model="price" />円<br />
      <p>金額は{{ price }}円です。</p>
      <p v-once>金額は{{ price }}円です。</p>
    </section>
  </section>

  <br />

  <section>
    <h2>レンダリング終了までマスタッシュ構文を非表示にする v-cloak</h2>
    <section>
      <p v-cloak>{{ hello }}</p>
    </section>
  </section>

  <br />
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
