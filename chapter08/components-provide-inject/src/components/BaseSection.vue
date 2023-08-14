<script setup lang="ts">
import { computed, inject } from 'vue'
import OneMember from './OneMember.vue'
import type { Member } from '../interfaces'

// 会員情報リストをInject
const memberList = inject('memberList') as Map<number, Member>
// 保有ポイントの合計の算出プロパティ
const totalPoints = computed((): number => {
  let total = 0
  for (const member of memberList.values()) {
    total += member.points
  }
  return total
})
</script>

<template>
  <section class="box">
    <h1>会員リスト</h1>
    <p>前会員の保有ポイントの合計: {{ totalPoints }}</p>
    <OneMember v-for="id in memberList.keys()" :key="id" :id="id" />
  </section>
</template>

<style scoped>
.box {
  border: orange 1px solid;
  margin: 16px;
  padding: 16px;
}
</style>
