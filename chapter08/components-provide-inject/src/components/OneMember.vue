<script setup lang="ts">
import { computed, inject } from 'vue'
import type { Member } from '../interfaces'

// Propsインターフェースの定義
interface Props {
  id: number
}

const props = defineProps<Props>()
const memberList = inject('memberList') as Map<number, Member>

// 該当する会員情報の取得 リアクティブなデータとするために算出プロパティにする
const member = computed((): Member | undefined => {
  return memberList.get(props.id) as Member
})

// Propsであるnoteを加工する算出プロパティ
const localNote = computed((): string => {
  return member.value?.note !== undefined ? member.value.note : '--'
})
</script>

<template>
  <section class="box" v-if="member">
    <h4>{{ member.name }} さんの情報</h4>
    <dl>
      <dt>ID</dt>
      <dd>{{ id }}</dd>
      <dt>メールアドレス</dt>
      <dd>{{ member.email }}</dd>
      <dt>保有ポイント</dt>
      <dd><input type="number" v-model.number="member.points" /></dd>
      <dt>備考</dt>
      <dd>{{ localNote }}</dd>
    </dl>
  </section>
</template>

<style scoped>
.box {
  border: pink 1px solid;
  margin: 16px;
  padding: 16px;
}
</style>
