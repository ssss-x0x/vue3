<script setup lang="ts">
import { computed } from "vue";
import { useCounterStore } from "./stores/counter";

const counterStore = useCounterStore();
const count = computed((): number => counterStore.count);
const doubleCount = computed((): number => counterStore.doubleCount);
const onIncrement = (): void => counterStore.increment();
const resetCount = (): void => {
  // $resetはsetup構文では使用できない
  // counterStore.$reset();

  // ので、$patchを使用する
  counterStore.$patch({ count: 0 });

  // もしくはvalueを0に書き換えることでリセットする
  counterStore.reset();
};
</script>

<template>
  <p>現在のポイント: {{ count }}</p>
  <p>現在のポイントをさらに倍: {{ doubleCount }}</p>
  <button @click="onIncrement">加算</button>
  <button @click="resetCount">リセット</button>
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
