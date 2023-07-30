# 第 5 章 双方向データバインディングとその他のディレクティブ

## 双方向のバインディング

- `v-bind` で利用するテンプレート変数 と `v-on:input` のイベントハンドラで利用するテンプレート変数で同一の変数を用いることで、双方向のデータバインディングが実現できる。
- `v-model` を使用することで下記双方向間のデータバインディングをシンプルに記述できる。

### テンプレート変数 → コントロール入力値

- フォームの `:value` にテンプレート変数を指定することで、自動的に変数の値が入力コントロールのデフォルトの value 値となる。

```
<script setup lang="ts">
import { ref } from 'vue'

const inputNameBind = ref('しんちゃん')
</script>

<template>
  <section>
    <input type="text" :value="inputNameBind" />
    {{ inputNameBind }}
  </section>
</template>
```

### コントロール入力値 → テンプレート変数

- input をイベントとして、イベントハンドラ `onInputName` で、入力値をテンプレート変数に格納する
- Vue のリアクティブシステムによって、テンプレート変数の変更後の値が p タグ内に表示される

```
<script setup lang="ts">
import { ref } from 'vue'

const inputNameOn = ref('ななし')
const onInputName = (event: Event): void => {
  const element = event.target as HTMLInputElement
  inputNameOn.value = element.value
}
</script>

<template>
  <section>
    <input type="text" @input="onInputName" />
    <p>{{ inputNameOn }}</p>
  </section>
</template>
```

## 双方向バインディングが使用できる範囲

- テキストエリアだけでなく、ラジオボタンやドロップダウンなど、他の入力コントロールでも `v-model` は利用できる。
- 入力コントロールのうち、ファイル選択コントロールの `file` は v-model は使えない。セキュリティ上、ファイルの受け取りだけがアプリケーションの仕事となるので双方向バインディングの概念自体が成り立たない。

## v-model の修飾子

| 修飾子 | 内容                                                         |
| ------ | ------------------------------------------------------------ |
| lazy   | input の代わりに change イベントで双方向データバインドを行う |
| number | 入力値を number 型に変換する                                 |
| trim   | 入力値の前後の余分な空白を取り除く                           |

- lazy を使うことで一通り入力を終えて、入力コントロールからフォーカスが離れてからデータバインディングが行えるようになる

## その他のデータバインディングのディレクティブ

### v-html

- Vue ではデータをバインドする場合に、自動で HTML エスケープを行うが、`v-html` ディレクティブを使用することでエスケープ処理を施さずに HTML 文字列をそのまま表示することができる。
- XSS 脆弱性を含む可能性があるため、v-html を使う場合は、プログラマが直接用意したデータなど信用できるものに限定する必要がある。

### v-pre

- マスタッシュ構文も含め、は以下のタグないのテンプレート記述をすべて無効化したまま表示するディレクティブ

### v-once

- 最初の 1 回だけデータバインドを行うディレクティブ

### v-cloak

- レンダリング途中でマスタッシュ構文がちらつくのを防止できる
