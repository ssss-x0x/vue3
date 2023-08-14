<script setup lang="ts">
import { ref, computed } from 'vue'

const memberTypeSelect = ref(1)

const memberTypeList = [
  { value: 1, name: '一般会員' },
  { value: 2, name: '特別会員' },
  { value: 3, name: '有料会員' }
]

const memberTypeName = computed(() => {
  const memberType = memberTypeList.find((item) => item.value === memberTypeSelect.value)
  return memberType ? memberType.name : ''
})
</script>

<template>
  <select v-model="memberTypeSelect">
    <option v-for="item in memberTypeList" :key="item.value" :value="item.value">
      {{ item.name }}
    </option>
  </select>
  <br />
  <p>選択されたリスト: {{ memberTypeName }}</p>
</template>

<style scoped></style>
