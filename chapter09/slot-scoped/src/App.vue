<script setup lang="ts">
import OneSection from './components/OneSection.vue'
</script>

<template>
  <section>
    <h1>子コンポーネントのSlotに記述されている値すべてを取得する</h1>
    <OneSection>
      <template v-slot:default="slotProps">
        <dl>
          <dt>名前</dt>
          <dd>{{ slotProps.member.name }}</dd>
          <dt>状況</dt>
          <dd>{{ slotProps.member.state }}</dd>
          <dt>備考</dt>
          <dd>{{ slotProps.member.note }}</dd>
          <dt>場所</dt>
          <dd>{{ slotProps.location.place }}</dd>
        </dl>
      </template>
    </OneSection>
  </section>
  <section>
    <h1>Slot Ptopsの分割代入</h1>
    <OneSection>
      <template v-slot:default="{ member }">
        <dl>
          <dt>名前</dt>
          <dd>{{ member.name }}</dd>
          <dt>状況</dt>
          <dd>{{ member.state }}</dd>
          <dt>備考</dt>
          <dd>{{ member.note }}</dd>
          <dt>場所</dt>
          <dd>{{ location?.place ?? '取得できませんでした。' }}</dd>
        </dl>
      </template>
    </OneSection>

    <OneSection>
      <template v-slot:default="{ member, location }">
        <dl>
          <dt>名前</dt>
          <dd>{{ member.name }}</dd>
          <dt>状況</dt>
          <dd>{{ member.state }}</dd>
          <dt>備考</dt>
          <dd>{{ member.note }}</dd>
          <dt>場所</dt>
          <dd>{{ location?.place ?? '取得できませんでした。' }}</dd>
        </dl>
      </template>
    </OneSection>
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
