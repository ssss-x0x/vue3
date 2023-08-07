<script setup lang="ts">
import { ref, computed } from 'vue'
import OneMember from './OneMember.vue'
import OneMemberWithDefault from './OneMemberWithDefault.vue'

interface Member {
  id: number
  name: string
  email: string
  points: number
  note?: string
}

// 会員リストデータを用意
const memberListInit = new Map<number, Member>()
memberListInit.set(33456, {
  id: 33456,
  name: '田中太郎',
  email: 'bow@example.com',
  points: 35,
  note: '初回入会特典あり。'
})
memberListInit.set(47783, { id: 47783, name: '鈴木二郎', email: 'mue@example.com', points: 53 })
const memberList = ref(memberListInit)

const totalPoints = computed((): number => {
  let total = 0
  for (const member of memberList.value.values()) {
    total += member.points
  }
  return total
})
</script>

<template>
  <h1>8.4 Props応用</h1>
  <h2>会員リスト</h2>
  <p>全会員の保有ポイントの合計: {{ totalPoints }}</p>
  <OneMember
    v-for="[id, member] in memberList"
    :key="id"
    :id="id"
    :name="member.name"
    :email="member.email"
    :points="member.points"
    :note="member.note"
  />
  <h2>デフォルト値を設定している会員リスト</h2>
  <OneMemberWithDefault
    v-for="[id, member] in memberList"
    :key="id"
    :id="id"
    :name="member.name"
    :email="member.email"
    :points="member.points"
    :note="member.note"
  />
</template>

<style scoped></style>
