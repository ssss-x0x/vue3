<script setup lang="ts">
import { ref, computed } from 'vue'

const msg = 'こんにちは世界'
const is_text_color_red = ref(true)
const is_bg_color_blue = ref(false)
const styles = ref({
  textColorRed: false,
  bgColorBlue: true,
  'text-color-pink': true
})

const computedStyles = computed((): { textColorRed: boolean; bgColorBlue: boolean } => {
  // 乱数を利用して0か1を生成(textColorRed用)
  const rand_text = Math.round(Math.random())

  // textColorRed プロパティの値を表す変数をtrueで用意
  let text_color_flg = true

  // 発生した乱数が0ならばfalseに変更
  if (rand_text === 0) text_color_flg = false

  // 乱数を利用して0か1を生成(bgColorBlue用)
  const rand_bg = Math.round(Math.random())

  // bgColorBlue プロパティの値を表す変数をtrueで用意
  let bg_color_flg = true

  // 発生した乱数が0ならばfalseに変更
  if (rand_bg === 0) bg_color_flg = false

  // それぞれのプロパティをオブジェクトにして返す
  return {
    textColorRed: text_color_flg,
    bgColorBlue: bg_color_flg
  }
})
</script>

<template>
  <!-- スタイルクラス適用をtrue/falseで指定 -->
  <p :class="{ textColorRed: true, bgColorBlue: true }">{{ msg }}</p>
  <p :class="{ textColorRed: is_text_color_red, bgColorBlue: is_bg_color_blue }">{{ msg }}</p>
  <p :class="{ textColorPink: true }">{{ msg }}</p> <!-- キャメル記法で書いてもケバブケースには変換されない -->
  <p :class="{ 'text-color-pink': true }">{{ msg }}</p> <!-- ので、シングルクォーテーションで囲う必要がある -->
  <p class="textSize24" :class="{ textColorRed: is_text_color_red, bgColorBlue: is_bg_color_blue }">
    {{ msg }}
  </p>
  <p class="textSize24" :class="styles">{{ msg }}</p>
  <p :class="computedStyles">{{ msg }}</p>
</template>

<style scoped>
.textColorRed {
  color: red;
}

.text-color-pink {
  color: pink;
}

.bgColorBlue {
  background-color: blue;
}

.textSize24 {
  font-size: 24px;
}
</style>
