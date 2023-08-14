# 第 9 章 子コンポーネント利用のバリエーション

## この章でやること

- 親コンポーネントが子コンポーネントを利用する方法のバリエーション「Slot」と「動的コンポーネント」について説明

## 子コンポーネントをカスタマイズする Slot

- Props 経由では HTML 要素そのものを渡すことができない。
  - Props で渡した値は、マスタッシュ構文で表示する際にエスケープされてしまうため HTML 要素ではなく、タグ形式の文字列として表示されてしまうため。
  - v-html ディレクティブを利用すれば HTML 要素としてレンダリングできるが、XSS 脆弱性が含まれてしまう。
  - v-for によって動的にレンダリングされた HTML 要素を渡すことはできない。
- そのため、HTML 要素をコンポーネント間でやり取りするためには`Slot`を利用する必要がある。
- slot は[Web の標準仕様](https://developer.mozilla.org/ja/docs/Web/HTML/Element/slot)として存在しており、Vue の slot は標準の仕組みを踏まえて拡張したもの。

### Slot の基本的な記述方法

- 親コンポーネントから渡された HTML 用を子コンポーネントで Slot として表示するには、 `<slot />`タグを利用する。
- コンポーネント呼び出し時は開始タグと終了タグを利用し、タグの間に子コンポーネントに渡したい HTML 要素を記述する。

### Slot のフォールバックコンテンツ

- Slot に対して HTML 要素が渡されなかった場合を想定してデフォルトの HTML 要素（フォールバックコンテンツ）を設定することが可能。

```
<slot>
 <!--ここにフォールバックコンテンツを記述する-->
</slot>
```

### テンプレート変数の所属先

- HTML 要素内でテンプレート変数を利用する場合、その変数は原則親コンポーネントで用意する必要がある。
- Slot 内の HTML 要素から参照できるのはコンポーネント内のテンプレート変数のみであり、別コンポーネントのテンプレート変数は参照できない。（親子関係でも同様）

## 複数の Slot を実現する名前付き Slot

### slot タグの追加

- 子コンポーネント内に`<slot>`タグを複数記述すると、同じ HTML 要素が挿入される。
- ひとつのコンポーネントに対して複数の箇所に異なる HTML 用を挿入したい場合は `名前付きSlot`として slot タグに名前をつける必要がある。

```
# 親コンポーネント
<ConponentName>
    <template v-slot:default> // #default のように省略記述もできる
        <!-- ここに名前のないSlot（default）のHTML要素を記述 -->
    </template>
    <template v-slot:slot名>
        <!-- ここに名前つきSlotのHTML要素を記述 -->
    </template>
</ConponentaName>

#子コンポーネント
<section>
    <slot>
        <!-- 名前のないSlotのフォールバックコンテンツ -->
    </slot>
    <slot name="slot名">
        <!-- 名前つきSlotのフォールバックコンテンツ -->
    </slot>
</section>
```

### データの受け渡しを逆転させるスコープ付き Slot（Slot Props）

- 原則、コンポーネント内の変数や処理はコンポーネント内で閉じておく必要がある。
- …が、Slot にはこの原則から外れる「親コンポーネントから子コンポーネント」の変数を利用するための仕組み「スコープ付き Slot」が設けられている。
- 子コンポーネントでデータを用意している場合に、親コンポーネントで HTML 要素を生成してから子コンポーネントで表示したい時に利用する。

```
# 親コンポーネント
<ConponentName>
    <template v-slot:default="slotProps">
        <p>{{ slopProps.member.name}}さん | {{ slotProps.member.age }}歳</p>
    </template>
</ConponentaName>

// 分割代入もできる
<ConponentName>
    <template v-slot:default="{ member }">
        <p>{{ member.name}}さん | {{ member.age }}歳</p>
    </template>
</ConponentaName>

#子コンポーネント
const memberInfo=reactive({
    name: 'taro',
    age: 20
})

// 省略
<section>
    <slot :member="memberInfo">
        {{ memberInfo.name }}さんです。
    </slot>
</section>
```

## 動的コンポーネント

- 読み込むコンポーネントをテンプレート変数で指定して動的に変更する仕組みを動的コンポーネント（Dynamic Components）と呼ぶ。
- `:is`ディレクティブ: 変数の値に該当するコンポーネントを読み込む
- `KeepAlive`コンポーネントを利用することで動的にレンダリングされたコンポーネントの状態を保持できるようになる。
  - KeepAlive タグで囲う場合、表示非表示でライフサイクル上 activate/deactivate を切り替えるので以前の状態が保持されている。
  - KeepAlive タグで囲わない場合、非表示にした際はライフサイクル上 ummounted 状態になり、すべてのデータなどが破棄される。
  - 静的なコンテンツの場合はデータを保持する必要がないので KeepAlive タグが不要になる。
