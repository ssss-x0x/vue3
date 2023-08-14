<script setup lang="ts">
import { ref } from 'vue'
import OneSection from './components/OneSection.vue'
import OneSectionFallBack from './components/OneSectionFallBack.vue'
import OneSectionDataScope from './components/OneSectionDataScope.vue'
import OneSectionSlotNamed from './components/OneSectionSlotNamed.vue'

const taro = ref('田中太郎')
const jiro = ref('山田二郎')

// 9.1.5 親でのレンダリング結果のSlot
const taroProblemListInit = ['電話が通じません。', '留守です。']
const taroProblemList = ref(taroProblemListInit)

// 9.2.3 slot名にテンプレート変数も使える
const slotName = ref('default')
</script>

<template>
  <section>
    <h2>9.1.2 Slotの利用</h2>
    <OneSection :name="taro">
      <p>連絡がつきません。</p>
    </OneSection>
  </section>
  <section>
    <h2>9.1.3 フォールバックコンテンツの利用</h2>
    <OneSectionFallBack :name="jiro" />
  </section>
  <section>
    <h2>9.1.4 テンプレート変数</h2>
    <OneSectionDataScope :name="taro">
      <p>{{ taro }}さんは連絡がつきません。</p>
    </OneSectionDataScope>
    <OneSectionDataScope :name="jiro" />
  </section>
  <section>
    <h2>9.1.5 親でのレンダリング結果のSlot</h2>
    <OneSectionDataScope :name="taro">
      <ul>
        <li v-for="problem in taroProblemList" :key="problem">
          {{ problem }}
        </li>
      </ul>
    </OneSectionDataScope>
    <OneSectionDataScope :name="jiro" />
  </section>
  <section>
    <h2>9.2 名前付きslot</h2>
    <OneSectionSlotNamed :name="taro">
      <template v-slot:default>
        <p>問題発生</p>
      </template>
      <template v-slot:detail>
        <ul>
          <li v-for="problem in taroProblemList" :key="problem">
            {{ problem }}
          </li>
        </ul></template
      >
    </OneSectionSlotNamed>
    <OneSectionSlotNamed :name="jiro" />
    <section>
      <h2>9.2.3 一部のSlotに入れるHTML要素だけを子コンポーネントへ渡すこともできる</h2>
      <OneSectionSlotNamed :name="jiro">
        <template #default>
          <p>微妙な問題発生</p>
        </template>
      </OneSectionSlotNamed>
    </section>
    <section>
      <h2>9.2.3 slot名にテンプレート変数も使える</h2>
      <OneSectionSlotNamed :name="jiro">
        <template v-slot:[slotName]>
          <p>ちょっと微妙な問題発生</p>
        </template>
      </OneSectionSlotNamed>
    </section>
  </section>
</template>

<style scoped></style>
