<script setup lang="ts">
import { ref, computed } from 'vue'
import OneSectionEmit from './OneSectionEmit.vue'
import OneMemberEmitValue from './OneMemberEmitValue.vue'
import OneMemberVmodel from './OneMemberVmodel.vue'

// 8.5.1 子から親への通信はイベント処理
const randInit = Math.round(Math.random() * 10)
const rand = ref(randInit)
const onCreateNewRand = (): void => {
  rand.value = Math.round(Math.random() * 10)
}

// 8.5.2 親コンポーネントにデータを渡す方法
interface Member {
  id: number
  name: string
  email: string
  points: number
  note?: string
}

// 会員リストデータを用意
const memberListInit = setMemberListInit()
const memberList = ref(memberListInit)

const totalPoints = computed((): number => {
  let total = 0
  for (const member of memberList.value.values()) {
    total += member.points
  }
  return total
})

const onIncrementPoint = (id: number): void => {
  const member = memberList.value.get(id)
  if (member !== undefined) {
    member.points++
  }
}

// 8.5.3 v-modelによる子から親への通信
const memberListInitVmodel = setMemberListInit()
const memberListVmodel = ref(memberListInitVmodel)

const totalPointsVmodel = computed((): number => {
  let total = 0
  for (const member of memberListVmodel.value.values()) {
    total += member.points
  }
  return total
})

// 会員リストデータを用意
function setMemberListInit() {
  const memberListInit = new Map<number, Member>()
  memberListInit.set(33456, {
    id: 33456,
    name: '田中太郎',
    email: 'bow@example.com',
    points: 35,
    note: '初回入会特典あり。'
  })
  memberListInit.set(47783, { id: 47783, name: '鈴木二郎', email: 'mue@example.com', points: 53 })
  return memberListInit
}
</script>

<template>
  <h1>8.5 子から親へのコンポーネント間通信</h1>
  <section>
    <h2>8.5.1 子から親への通信はイベント処理</h2>
    <p>親コンポーネントで乱数を表示 {{ rand }}</p>
    <OneSectionEmit :rand="rand" @createNewRand="onCreateNewRand" />
  </section>
  <section>
    <h2>8.5.2 親コンポーネントにデータを渡す方法</h2>
    <p>全会員の保有ポイントの合計: {{ totalPoints }}</p>
    <OneMemberEmitValue
      v-for="[id, member] in memberList"
      :key="id"
      :id="id"
      :name="member.name"
      :email="member.email"
      :points="member.points"
      :note="member.note"
      @incrementPoint="onIncrementPoint"
    />
  </section>
  <section>
    <h2>8.5.3 v-modelによる子から親への通信</h2>
    <p>全会員の保有ポイントの合計: {{ totalPointsVmodel }}</p>
    <OneMemberVmodel
      v-for="[id, member] in memberListVmodel"
      :key="id"
      :id="id"
      :name="member.name"
      :email="member.email"
      v-model:points="member.points"
      :note="member.note"
    />
  </section>
</template>

<style scoped></style>
