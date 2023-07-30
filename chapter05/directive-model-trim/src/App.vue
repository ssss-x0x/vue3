<script setup lang="ts">
import { ref } from 'vue'

const trimedText = ref('')
const lazyText = ref('')
const numberText = ref(0)
const notNumberText = ref(0)
</script>

<template>
  <section>
    <input type="text" v-model.trim="trimedText" /><br />
    <p>トリムされた入力文字列:{{ trimedText }}</p>
  </section>

  <br />

  <section>
    <input type="text" v-model.lazy="lazyText" /><br />
    <p>入力が終わってからバインディングされる文字列:{{ lazyText }}</p>
  </section>

  <br />

  <section>
    <input type="text" v-model.number="numberText" /><br />
    <p>
      number修飾子をつけてnumber型に変換される文字列:{{ numberText }} 型:{{ typeof numberText }}
    </p>
  </section>
  <br />

  <section>
    <input type="text" v-model="notNumberText" /><br />
    <p>
      数字で入力されたけど型はstringのままの文字列:{{ notNumberText }} 型:{{ typeof notNumberText }}
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
