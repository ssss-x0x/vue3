<script setup lang="ts">
import { ref } from 'vue'

const memberType = ref(1)

const memberTypeList = [
  { value: 1, name: '一般会員' },
  { value: 2, name: '特別会員' },
  { value: 3, name: '有料会員' }
]
</script>

<template>
  <label v-for="item in memberTypeList" :key="item.value">
    <input type="radio" name="memberType" :value="item.value" v-model="memberType" />
    {{ item.name }}
  </label>
</template>

<style scoped></style>
