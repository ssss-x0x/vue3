# 第 6 章 制御のディレクティブ

## 条件分岐のディレクティブ v-if

- 条件に合致した場合にタグがレンダリングされる
- 可読性の観点から、複雑な条件式の場合は算出プロパティを活用するのが良い（directive-conditional-basic の表示 ③ を参照）
- `v-else-if`と`v-else`で「条件に合致したいずれかのタグを表示する」ことができるが、`v-if`を記述したタグを常に連続させる必要がある。
- 条件分岐のためにコードをまとめたい場合は`template`を用いる。ディレクティブのために無意味な div, span などのタグを生むことは避けた方が良い。

### v-show と v-if の違い

- レンダリング結果が異なる。
  ||v-show|v-if|
  |---|---|---|
  |条件に合致する場合|タグが出力される|タグが出力される|
  |条件に合致しない場合|タグが出力され、`style=display:none;`で非表示にする|タグ自体が出力されない|
- `v-show` は表示・非表示の切り替えコストが低いので頻繁に切り替えが発生する場合に使うのが良い
- `v-if` では条件に合致しなかった場合のレンダリングがまったく発生しないため、表示・非表示があらかじめ決まっている場合に使うのが良い
- レンダリングされない `template` タグでは、タグでの出力が必要となる `v-show`が使えない。

## ループのディレクティブ v-for

```
基本構文
v-for="(各要素を格納する変数,インデックス値を格納する変数) in ループしたい変数" :key="要素を識別するための値"
※ Vueでは各要素を格納する変数を「エイリアス」と呼ぶ
```

- key: ループ処理によって生成された各要素を Vue 本体から識別するため、キー文字列をバインドする記述。
- key はループ処理後、一意となる文字列であることが求められる。
- オブジェクトのループも連想配列と同様の構文で実現できる

```
連想配列でインデックス値を利用する場合のv-forディレクティブ
v-for="(各要素を格納する変数,各要素のキーを格納する, インデックス値を格納する変数) in ループしたい変数" :key="要素を識別するための値"
```

### Map のループ

- Map を利用するには Map を new して set()する必要がある
- Map を利用するとキーとして id を使用できる（get メソッドでキーを指定して取り出せる）ため、管理がしやすくなる。

```
【例】
const cocktailListInit = new Map<number, string>()
cocktailListInit.set(2345, 'ホワイトレディ')
cocktailListInit.set(4412, 'ブルーハワイ')
...

v-for="[id, item] in cocktailListInit" :key="id"
```

### カウンタ変数を利用したループ

- 一定の回数ループを行いたい場合、終端の値のみを記述する。（西暦の年を一覧で表示したい場合などに用いる）

```
v-for="カウンタ変数 in 終端の値"
```

## リスト操作

### ループ対象データの絞り込み

- ループ内で v-if 制御をかける方法もあるが、 「v-for と v-if を同時に記述してはいけない」というスタイルガイドに反することになる。
- そのため、算出プロパティを用いて絞り込みを行うのが良い。

### Map オブジェクト内のデータ変更

- オブジェクト内のデータを変更するだけで、リアクティブに表示内容も変わる。リスト内のデータも同様。