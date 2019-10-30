# CSS設計ガイドライン v0.2.1

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [レイヤー](#%E3%83%AC%E3%82%A4%E3%83%A4%E3%83%BC)
  - [Foundation【基礎】](#foundation%E5%9F%BA%E7%A4%8E)
  - [Layout【レイアウト】](#layout%E3%83%AC%E3%82%A4%E3%82%A2%E3%82%A6%E3%83%88)
  - [Object【オブジェクト】](#object%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
    - [Module【汎用オブジェクト】](#module%E6%B1%8E%E7%94%A8%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
    - [Component【複合オブジェクト】](#component%E8%A4%87%E5%90%88%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
    - [Package【ユニークオブジェクト / 統合オブジェクト】](#package%E3%83%A6%E3%83%8B%E3%83%BC%E3%82%AF%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88--%E7%B5%B1%E5%90%88%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
    - [Page【ページ】](#page%E3%83%9A%E3%83%BC%E3%82%B8)
    - [Utility【ユーティリティ】](#utility%E3%83%A6%E3%83%BC%E3%83%86%E3%82%A3%E3%83%AA%E3%83%86%E3%82%A3)
- [禁止と制限](#%E7%A6%81%E6%AD%A2%E3%81%A8%E5%88%B6%E9%99%90)
  - [カスケーディングの制限](#%E3%82%AB%E3%82%B9%E3%82%B1%E3%83%BC%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0%E3%81%AE%E5%88%B6%E9%99%90)
- [基本構成](#%E5%9F%BA%E6%9C%AC%E6%A7%8B%E6%88%90)
  - [ディレクトリ構成](#%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E6%A7%8B%E6%88%90)
  - [style.scss](#stylescss)
- [コーディングガイドライン](#%E3%82%B3%E3%83%BC%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%AC%E3%82%A4%E3%83%89%E3%83%A9%E3%82%A4%E3%83%B3)
  - [命名規則](#%E5%91%BD%E5%90%8D%E8%A6%8F%E5%89%87)
    - [BEM](#bem)
    - [label](#label)
    - [JavaScript](#javascript)
  - [コードの自動フォーマット](#%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AE%E8%87%AA%E5%8B%95%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## レイヤー

詳細度の管理の円滑化と、再利用性・拡張性の拡充の目的のため、以下のルールに基づき、各スタイルをレイヤーごとに分類する。

<table>
  <thead>
    <tr>
      <th align="left">Lv</th>
      <th align="left" colspan="2">レイヤー</th>
      <th align="left" colspan="2">役割</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">1</td>
      <td align="left" colspan="2">Foundation</td>
      <td align="left">基礎となるスタイル</td>
      <td align="center">詳細度 低 / 抽象的 / 汎用的</td>
    </tr>
    <tr>
      <td align="center">2</td>
      <td align="left" colspan="2">Layout</td>
      <td align="left">汎用的な配置のパターン</td>
      <td align="center">↑</td>
    </tr>
    <tr>
      <td align="center">3</td>
      <td align="left">Object</td>
      <td align="left">Module</td>
      <td align="left">最小単位のオブジェクトの見栄え</td>
      <td align="center">｜</td>
    </tr>
    <tr>
      <td align="center">4</td>
      <td align="left">Object</td>
      <td align="left">Component</td>
      <td align="left">汎用的なオブジェクトの見栄え</td>
      <td align="center">｜</td>
    </tr>
    <tr>
      <td align="center">5</td>
      <td align="left">Object</td>
      <td align="left">Package</td>
      <td align="left">専用的なオブジェクトの配置・見栄え</td>
      <td align="center">｜</td>
    </tr>
    <tr>
      <td align="center">6</td>
      <td align="left" colspan="2">Page</td>
      <td align="left">特定のページでのみ使用する部品</td>
      <td align="center">↓</td>
    </tr>
    <tr>
      <td align="center">7</td>
      <td align="left" colspan="2">Utility</td>
      <td align="left">ヘルパースタイル</td>
      <td align="center">詳細度 高 / 具体的 / 専用的</td>
    </tr>
  </tbody>
</table>

- 上位レベルのレイヤーほど、**CSSの詳細度**が高くなる。
- 上位レベルのレイヤーほど、**抽象的でなく具体的**になる。
- `Utility`レイヤーを除き、上位レベルのレイヤーほど、**汎用的でなく専用的**になる。
- 各レイヤーで定義されたひとつのスタイルのまとまりを**レイヤー要素**と定義する。

### Foundation【基礎】

リセットCSS、Webフォントの定義、タグの基本的なスタイルの定義など、基礎となるスタイルが帰属するレイヤー。

``` scss
:root {
  font-size: $_font-size;
}

body {
  font-family: $_font-family;
  line-height: $_line-height;
  color: $_text-color;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-text-size-adjust: 100%;
}

a {
  color: $_text-link-color;
  text-decoration: none;
}
```

### Layout【レイアウト】

**クラス名の先頭に`l_`を付与する。**

グリッド、コンテンツブロックのセンタリングなど、**汎用的な配置のパターン**が帰属するレイヤー。

- 自身の基本的な見栄え（背景色など）は、ここで定義して良い。

``` scss
.l_container {
  width: 1200px;
  background-color: #fff;
  margin: 0 auto;
  ...
}
```

### Object【オブジェクト】

サイトの主要構成部品の見栄え、配置のパターンが帰属するレイヤー。

- 詳細度、要素単位の規模、汎用性などの種類によって、更に以下の子レイヤーに区分される。

#### Module【汎用オブジェクト】

**クラス名の先頭に`m_`を付与する。**

ボタン、アイコン、見出し、表、リストなど、最小単位の**汎用的なオブジェクト**が帰属するレイヤー。

- 見栄えに関わるスタイルを定義する。
- 配置に関わるスタイル（固定の幅やマージンなど）は、親となる上位レベルのレイヤーで定義する。
- 使用箇所を限定するようなクラス名は避ける。

``` scss
.m_btn {
  ...
  &._disabled {
    ...
  }
}
```

#### Component【複合オブジェクト】

**クラス名の先頭に`c_`を付与する。**

タブ、モーダル、ページャー、記事リンクのリッチカードなど、複数の単一オブジェクトやタグの組み合わせで構成される**複合的なオブジェクト**が帰属するレイヤー。

- 見栄えに関わるスタイルを定義する。
- 自身の配置に関わるスタイルは、親となる上位レベルのレイヤーで定義する。
- 機能や見栄えが予測できるようなクラス名をつける。

``` scss
.c_article-card {
  ...
  .m_btn {
    ...
  }
}
```

#### Package【ユニークオブジェクト / 統合オブジェクト】

**クラス名の先頭に`p_`を付与する。**

ヘッダー、フッター、サイドバー、メインコンテンツエリアのコンテナーなど、各ページにおいて<strong>一意なオブジェクト（ユニークオブジェクト）</strong>または<strong>複数の単一または複合オブジェクトの配置のパターン（統合オブジェクト）</strong>が帰属するレイヤー。

- ユニークオブジェクトには、ページ上の場所や機能が予測できるようなクラス名をつける。
- 統合オブジェクトには、内包するオブジェクトや機能が予測できるようなクラス名をつける。

``` scss
.p_header {
  ...
}
```

``` scss
.p_article-cards {
  ...
  .c_article-card {
    ...
  }
}
```

#### Page【ページ】

**クラス名の先頭に`{ページ名}_`を付与する。**

特定のページでのみ使用する部品の見栄え、配置のパターンが帰属するレイヤー。

- 新たなページの追加や既存ページの更新などによって、同じような部品が登場した場合は、他のレイヤーで再定義できないか検討する。

``` scss
.home_visual {
  ...
}
```

#### Utility【ユーティリティ】

**クラス名の先頭に`u_`を付与する。**

Modifierで解決することが難しいまたは適切ではない、わずかなスタイルを調整するスタイルが帰属するレイヤー。

- 本レイヤーのみ`!important`ルールの使用が可能。

``` scss
.u_fs-smaller {
  font-size: smaller !important;
}
```

## 禁止と制限

### カスケーディングの制限

レイヤー要素間のカスケーディングは、上位レベルのレイヤー要素による下位レベルのレイヤー要素のカスケーディングを除き、禁止とする。

``` scss
// (1)
// 下位レベルのレイヤー要素で上位レベルのレイヤー要素をカスケーディングしている
// 上位レベルのレイヤー要素ほど詳細度が高くなるという本ガイドラインのルールが曖昧になってしまう
.c_component {
  .p_package {
    ...
  }
}
```

```scss
// (2)
// 同位レベルのレイヤー要素同士でカスケーディングしている
// 同位レベルのレイヤー要素同士に依存関係をもたせると、挙動の予測が困難になってしまう
.c_a-component {
  .c_b-component {
    ...
  }
}
```

``` jsx
// (2)の例と同様
<div class="c_component-a c_component-b">
  ...
</div>
```

## 基本構成

### ディレクトリ構成

``` shell
├── lib/
└── app/
│   ├── founadtions/    # Foundationレイヤー
│   ├── layouts/        # Layoutレイヤー
│   ├── objects/
│   │   ├── components/ # Componentレイヤー
│   │   ├── modules/    # Moduleレイヤー
│   │   └── packages/   # Packageレイヤー
│   ├── pages/          # Pageレイヤー
│   ├── utilities/      # Utilityレイヤー
│   ├── vendors
│   └── variable.scss/  # グローバル変数
└── style.scss
```

- `vendors`は、サードパーティのCSSや、jQueryプラグインなどのサードパーティライブラリで定義されたスタイルをオーバーライドするスタイルを記述したCSS（SCSS）ファイルを配備するディレクトリ。当該スタイルは本ガイドラインの適用対象外とする。

### style.scss

- 設定と各レイヤーの`@import`順を変更しないこと。
- `vendors`は、任意の位置で`@import`して良い。

## コーディングガイドライン

### 命名規則

#### BEM

基本的にはBEMのルールを継承するが、可読性の向上のため、以下にように独自のルールを設ける。

- `Block__Element1__Element2`のようにElementの連結はせず、`Block__Element1-Element2`または`Block__Element3`のようにする。
- Modifier（--）は使用せず、アンダースコアから始まる具体的な名前をつけたクラスを定義し、マルチクラスで指定する。

``` html
<ul class="p_article-cards">
  <li class="c_article-card"></li>
  <li class="c_article-card _highlight"></li>
</ul>
```

```scss
.c_article-card {
  &._highlight {
      // Modifier style
    }
}
```

#### label

labelタグのfor属性値で使用するIDには、`label_`プレフィックスを付与する。

- このセレクタにはスタイルを定義しない。

#### JavaScript

JavaScriptで操作するためのセレクタとしてID・Classセレクタを使用する場合には、セレクタ名に`js_`プレフィックスを付与する。

- 特に問題のない限り、Classを使用する。
- このセレクタにはスタイルを定義しない。

### コードの自動フォーマット

[Visual Studio Code](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)の場合は、以下のプラグインで保存時に自動的にコード整形ができるようになる。
- [EditorConfig for VS Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [stylelint-plus](https://marketplace.visualstudio.com/items?itemName=hex-ci.stylelint-plus)
