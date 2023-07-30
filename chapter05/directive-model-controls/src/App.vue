<script setup lang="ts">
import { ref } from 'vue'

const inputTextArea = ref('テキストエリアへの入力文字。 \n 改行も加えてみる。')
const memberType = ref(1)
const memberTypeSelect = ref(1)
const memberTypes = [
  { value: 1, label: '通常会員' },
  { value: 2, label: '特別会員' },
  { value: 3, label: '優良会員' }
]
const isAgreed = ref(false)
const isAgreed01 = ref(0)
const selectedOS = ref([1])
const selectedOSSelect = ref([2])
const selectedOSs = [
  { value: 1, label: 'macOS' },
  { value: 2, label: 'Windows' },
  { value: 3, label: 'Linux' },
  { value: 4, label: 'iOS' },
  { value: 5, label: 'Android' }
]
</script>

<template>
  <section>
    <textarea v-model="inputTextArea"></textarea>
  </section>

  <br />

  <section>
    <label v-for="member in memberTypes" :key="member.value"
      ><input type="radio" name="memberType" :value="member.value" v-model="memberType" />{{
        member.label
      }}</label
    >
    <br />
    <p>選択されたラジオボタン: {{ memberType }}</p>
  </section>

  <br />

  <section>
    <select v-model="memberTypeSelect">
      <option v-for="member in memberTypes" :key="member.value" :value="member.value">
        {{ member.label }}
      </option>
    </select>
    <br />
    <p>選択されたリスト: {{ memberTypeSelect }}</p>
  </section>

  <br />

  <section>
    <label><input type="checkbox" v-model="isAgreed" />同意する</label>
    <p>同意の結果: {{ isAgreed }}</p>
  </section>

  <br />

  <section>
    <label
      ><input type="checkbox" v-model="isAgreed01" true-value="1" false-value="0" />同意する</label
    >
    <p>同意の結果: {{ isAgreed01 }}</p>
  </section>

  <br />
  <section>
    <label v-for="os in selectedOSs" :key="os.value"
      ><input type="checkbox" v-model="selectedOS" :value="os.value" /> {{ os.label }}</label
    >
    <p>選択されたOS: {{ selectedOS }}</p>
  </section>

  <br />

  <section>
    <select v-model="selectedOSSelect" multiple>
      <option v-for="os in selectedOSs" :key="os.value" :value="os.value">
        {{ os.label }}
      </option>
    </select>
    <p>選択されたOS: {{ selectedOSSelect }}</p>
  </section>
</template>

<style scoped>
section {
  gap: 1em;
}
</style>
