title: Getting Started
type: guide
order: 2
---

## Introduction

Vue.js はインタラクティブなウェブインターフェースを作るためのライブラリーです。

技術的に、Vue.js はMVVM pattern の [ViewModel](#ViewModel) layer に注目しています。[ViewModel](#ViewModel) layer は双方向バインディングによって [View](#View) と [Model](#Model) を接続します。実際の DOM 操作と出力の形式は[Directives](#Directives) と [Filters](#Filters)によって抽象化されています。

Vue.js の哲学的なゴールは、可能な限り簡単なAPIを通じて、反応性の良いデータバインディングの利点と構成可能なviewのコンポーネントを提供することです。Vue.jsは万能なフレームワークではありません。 Vue.jsは単純かつ自由自在なview layerになるようにデザインされています。Vue.jsを単体でラピッドプロトタイピングができます。特別な front-end stack 用のライブラリー達と一緒に使ったり組み合わせたりもできます。Vue.jsは Firebase のようなノーバックエンドサービスとも合性が良いです。

Vue.js の API は [AngularJS]、[KnockoutJS]、[Ractive.js]、 [Rivets.js]に強く影響を受けています。それらと似てはいますが、単純さと機能性のちょうど良いスィートスポットを見つけることによって、Vue.jsはそれらのライブラリーに対して価値ある代変手段になりうると私は信じています。

貴方は、その他のライブラリーの表現に既に慣れているかもしれませんが、それらの表現の記法がVue.js の文脈において意味するところとは違っているかもしれませんので、以下に示すコンセプトの全体像に目を通してみてください。

## Concepts Overview

### ViewModel

Model と Viewを同期するオブジェクト。 Vue.js において, 全ての Vue インスタンスはViewModelです。 それらは `Vue` コンストラクターかそのサブクラスでインスタンス化されます:

```js
var vm = new Vue({ /* options */ })
```

これは貴方がVue.jsをつかって開発するときに初めて出会うオブジェクトです。詳細は [The Vue Constructor](/api/) を見てください。

### View

Vue インスタンスによって管理される実際の DOM.

```js
vm.$el // The View
```

Vue.js は DOM ベースのテンプレーティングを使います。各々のVue インスタンスはassociated with a 対応する DOM 要素と関連づいています。Vue インスタンスが作られると、必要なデータバインディングを設定している間、Vue インスタンスはその親要素の全ての子ノードを再帰的に巡回します。

Vue.jsを使っているときに、貴方が貴方自身でDOM に触れることはcustom directives (後述)を除いて殆どありません。 View の更新はデータが変わったときに自動的に行われます。これらのView の更新は、textNodeに至る精度を持った高い粒度（？）で行われます。 これらは高性能化のために、バッチ化されて非同期実行されてもいます。

### Model

若干修正されたプレーンな JavaScript オブジェクト。

```js
vm.$data // The Model
```

Vue.jsにおいて、Model は単純にプレーンな JavaScript オブジェクトか**data objects**です。貴方はそれらのプロパティと、それらが変更されるかを観察しているVue インスタンスを操作できます。Vue.js はdata objectsのプロパティをES5 getter/settersに変換することによって、透過的な応答（？）を実現します。 ダーティーチェックは必要ありませんし、Viewを更新するために、明示的なシグナルを Vue に送る必要もありません。 データが変更されたときはいつでも、次のフレームでViewは更新されます。

Vue インスタンスは、それらが観察している data objects の全てのプロパティをプロキシしています。 そのため、一度オブジェクト `{ a: 1 }` が観察されれば、 `vm.$data.a` と`vm.a` の両方が同じ値を返します。また、`vm.a = 2` に設定すると `vm.$data` が変わります.

data objectsは適当な位置で変化します。そのため、参照によってそれらを変更することは、`vm.$data` を変更することと同じ効果を持っています. この事が、複数の Vue インスタンスがデータの同じ部分を観察することを可能にしています。より広い応用としては、 Vue インスタンスは純粋なviewとして使われること、and externalize the data 操作のロジックをより離散的なstore layerに具体化すること（？）、も推奨されます。

ここでの問題は、一度観察が始まったら、Vue.js はプロパティの新規追加と削除を検出できないことです。
この問題を避けるために、観察されたオブジェクトは`$add` と `$delete` メソッドで追加削除されます。
### Directives

Vue.js が DOM 要素についての何かをすることを伝えている プレフィックスのついた HTML 属性

```html
<div v-text="message"></div>
```

ここでHere the div 要素は valueが `message` `v-text` directiveを持っています。 これはVue.js が、divの textContent がVue インスタンスの`message` プロパティと同期していることを、保っていることを伝えています。

Directive は任意の DOM 操作をカプセル化できます。例えば、`v-attr` は要素の属性を操作しますし、`v-repeat` はアレイに基づいて要素をクローンしますし、, `v-on` はイベントリスナーを随行します。これらは後にまとめます。

### Mustache Bindings

貴方はテキストと属性の両方においてmustache-style バインディングを使うこともできます。それらは内部で、`v-text`ディレクティブ と `v-attr` ディレクティブに翻訳されます。例えば:

```html
<div id="person-{{id}}">Hello {{name}}!</div>
```

この書き方は便利ですが、いくつか注意しなければならないことがあります:

<p class="tip"> `<image>` 要素の `src` 属性は、値が設定されたときにHTTP リクエストを作成します。そのため、テンプレートが初めに解析されたときに、404の結果が返ってきます. この場合は、`v-attr` を使うのが良いです。 </p>

<p class="tip">Internet Explorer は、HTMLを解析しているときに、`style`属性の無効なインラインを削除します。 そのためIEをサポートしたい場合、 インラインCSS をバインディングするときにはいつも`v-style`を使ってください。</p>

エスケープされていない（？）HTMLに対して3重のmustacheを使うことができ、それは内部で`v-html` に翻訳されます:

``` html
{{{ safeHTMLString }}}
```

しかしながら、this can open up windows for potential XSS attacks, therefore it is suggested that you only use triple mustaches when you are absolutely sure about the security of the data source, or pipe it through a custom filter that sanitizes untrusted HTML.

Finally, you can add `*` to your mustache bindings to indicate a one-time only interpolation, which does not react to data changes:

``` html
{{* onlyOnce }}
```

### Filters

Filters are functions used to process the raw values before updating the View. They are denoted by a "pipe" inside directives or bindings:

```html
<div>{{message | capitalize}}</div>
```

Now before the div's textContent is updated, the `message` value will first be passed through the `capitalize` function. For more details see [Filters in Depth](/guide/filters.html).

### Components

In Vue.js, every component is simply a Vue instance. Components form a nested tree-like hierarchy that represents your application interface. They can be instantiated by a custom constructor returned from `Vue.extend`, but a more declarative approach is registering them with `Vue.component(id, constructor)`. Once registered, they can be declaratively nested in other Vue instance's templates with the `v-component` directive:

``` html
<div v-component="my-component">
  <!-- internals handled by my-component -->
</div>
```

This simple mechanism enables declarative reuse and composition of Vue instances in a fashion similar to [Web Components](http://www.w3.org/TR/components-intro/), without the need for latest browsers or heavy polyfills. By breaking an application into smaller components, the result is a highly decoupled and maintainable codebase. For more details, see [Component System](/guide/components.html).

## A Quick Example

``` html
<div id="demo">
  <h1>{{title | uppercase}}</h1>
  <ul>
    <li
      v-repeat="todos"
      v-on="click: done = !done"
      class="{{done ? 'done' : ''}}">
      {{content}}
    </li>
  </ul>
</div>
```

``` js
var demo = new Vue({
  el: '#demo',
  data: {
    title: 'todos',
    todos: [
      {
        done: true,
        content: 'Learn JavaScript'
      },
      {
        done: false,
        content: 'Learn Vue.js'
      }
    ]
  }
})
```

**Result**

<div id="demo"><h1>&#123;&#123;title | uppercase&#125;&#125;</h1><ul><li v-repeat="todos" v-on="click: done = !done" class="&#123;&#123;done ? 'done' : ''&#125;&#125;">&#123;&#123;content&#125;&#125;</li></ul></div>
<script>
var demo = new Vue({
  el: '#demo',
  data: {
    title: 'todos',
    todos: [
      {
        done: true,
        content: 'Learn JavaScript'
      },
      {
        done: false,
        content: 'Learn Vue.js'
      }
    ]
  }
})
</script>

Also available on [jsfiddle](http://jsfiddle.net/yyx990803/yMv7y/).

You can click on a todo to toggle it, or you can open your Browser's console and play with the `demo` object - for example, change `demo.title`, push a new object into `demo.todos`, or toggle a todo's `done` state.

You probably have a few questions in mind now - don't worry, we'll cover them soon. Next up: [Directives in Depth](/guide/directives.html).

[AngularJS]: http://angularjs.org
[KnockoutJS]: http://knockoutjs.com
[Ractive.js]: http://ractivejs.org
[Rivets.js]: http://www.rivetsjs.com
