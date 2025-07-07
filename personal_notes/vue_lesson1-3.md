# Vue.js入門 Lesson1～3

～目次～

- <a href="#L1">Lesson1</a>
- <a href="#L2">Lesson2</a>
- <a href="#L3">Lesson3</a>

---
<a name="#L1"></a>
<br><br>

# 【Vue.js入門#1】Vue.jsでWebアプリケーションを作ろう！/基礎解説&環境構築【Vue3】

https://www.youtube.com/watch?v=7esDY8YIsQk&list=PL33OZZ24O4xDJ-_mqltklx8-9DK79iDOj&index=1

## Vue.jsって何？
フロントエンドのJavaScriptフレームワーク。
アプリケーションのUI開発に適している。
React, jQuery, AngularもJavaScriptフレームワーク。

## Vue.jsの特徴

### 1.学習コストが低い

日本語の公式サイトが用意されていることや、構文が簡単なことから学習コストが低く、ほかのフレームワークと比較して簡単に始められる。

### 2.仮想DOMによって高速に処理することができる。

```
DOM (Document Object Model)
プログラム(JavaScript)から、HTMLやXMLを扱うための機能。
WEBページの要素とプログラムとをつなぐ橋渡し役。
```

```
仮想DOM
実際のDOMと同じ構造を持つが、JavaScriptのオブジェクトとして実装される。
ページを切り替えるときは、画面(DOM)全体を再描画するのではなく、仮想DOMを使って差分のみを更新するため、高速に画面を切り替えることができる。
仮想DOMはReactでも採用されている。
```


### 3.シンプルで拡張性がある。

シンプルな設計、かつ柔軟性が高く、ほかのライブラリと組み合わせて使うこともできる。



### 4.データを同期できる。

画面で表示（HTML）するデータと、処理で使うデータと紐づけて扱うことができるため、簡単にコードを書くことができる。


## WSL+Dockerで環境構築する場合はこちらを参照

●　Docker上にVue.js開発環境を作る

https://qiita.com/taketakekaho/items/8e6d16f29ea198f24d61


●　WSLにDocker+VS Codeを導入する

https://qiita.com/Lintaro/items/d30d10d29212e0c5be47


下記のメッセージが表示され「http://localhost:8080/」にアクセスして、WELCOME画面が出ればOK

```javascript

 DONE  Compiled successfully in 5321ms                                                                                             12:23:23 PM


  App running at:
  - Local:   http://localhost:8080/

  It seems you are running Vue CLI inside a container.
  Access the dev server via http://localhost:<your container's external mapped port>/

  Note that the development build is not optimized.
  To create a production build, run yarn build.
```


## ファイル構成

```shell
.
├── README.md
├── babel.config.js
├── jsconfig.json
├── node_modules
├── package.json
├── public
│   ├── favicon.ico
│   └── index.html  // ←　画面に表示されるHTML
├── src
│   ├── App.vue
│   ├── assets
│   ├── components
│   └── main.js
├── vue.config.js
└── yarn.lock
```

### index.htmlとApp.vueの内容

#### index.html

```html

  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>   <!-- ← このdivタグで、src/App.vueの中身が紐づいている -->
    <!-- built files will be auto injected -->
  </body>

```


#### src/App.vue

```html

<!-- 標準HTMLにはないタグが定義されている。これがコンポーネントと呼ばれVue.js必須の概念になる。 -->

<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

```


<br>  <br>  

--------------------
--------------------
--------------------

<br>  <br>  

<a name="#L2"></a>
<br><br>

# 【Vue.js入門#2】Vue.jsでWebアプリケーションを作ろう！/ファイル構成&コンポーネント【Vue3】

https://www.youtube.com/watch?v=antdikF8J4g&list=PL33OZZ24O4xDJ-_mqltklx8-9DK79iDOj&index=2




## コンポーネントとは？

コンポーネント・・・(英)「構成要素」「部品」「成分」

→　Vueアプリケーション画面を構成する部品のことを指す。パーツごとにHTML,JS,CSSすべてをひとまとめにして扱う。


![](./images/Lesson02-01.png)


→　いちばん外側（親）になるコンポーネントは、**ルートコンポーネント**と呼ばれる。


### コンポーネントを使うメリット

1. 再利用しやすく、効率的に開発できる。
2. バグの影響範囲を見つけやすい。
3. 変更があったときにまとめて補正できる。(コンポーネントの中身を編集するだけで全体に反映される)


##  Vueプロジェクトの構成

```shell
.
├── README.md
├── babel.config.js
├── jsconfig.json
├── node_modules
├── package.json
├── public
│   ├── favicon.ico
│   └── index.html  // ←　画面に表示されるHTML
├── src
│   ├── App.vue
│   ├── assets
│   ├── components
│   └── main.js
├── vue.config.js
└── yarn.lock


```


#### index.html

```html
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>   <!-- ← このdivタグで、src/App.vueの中身が紐づいている -->
    <!-- built files will be auto injected -->
  </body>
```


#### src/main.js

Vueアプリケーションの初期化などを行う。エントリーポイント（*プログラムが開始される場所*）として機能する。

```javascript
// vueモジュールから、createApp関数、さらにApp.vueからAppコンポーネントをインポート

import { createApp } from 'vue'
import App from './App.vue'

// createAppとは、Vueインスタンスを生成する関数。カッコ内はルートコンポーネントを指定している。　
// mount（結びつけ）とは、index.html内の「id=#app」に結びつけを行うことを指示している。
createApp(App).mount('#app')
```

#### src/App.vue

Vueアプリケーションのルートコンポーネント。

他のコンポーネントを含み、アプリケーション全体のレイアウトなどを決める。


Vueファイルは、

- script部分(JavaScript)
- template部分(HTML)
- style部分(CSS)

に分けることができる。



```html

<!-- index.htmlにマウントされ画面に表示されるHTMLを <template>タグ中に書く -->
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>


<script>
/*使用するコンポーネントをimportする。*/
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
/* HTMLの見た目を指定するCSSを定義する。*/
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

#### src/components配下

コンポーネントのVueファイルが入っている。

```sh
./components/
└── HelloWorld.vue
```


#### src/assets配下

画像やCSSを入れる。

```sh
./assets
└── logo.png
```

##  コンポーネントを作ってみる


### src/components/HelloWorld.vue

最低限＜tenplate＞タグがあればコンポーネントとして使用できる

```html

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
</style>

```


### src/components/の下に「TestComponent.vue」を作ってみる


空白vueファイルに下記のタグを記述する。



```html
<!-- src/components/TestComponent.vue -->
<template>
    <p>コンポーネントです。</p>
</template>
```

→　次に「TestComponent.vue」を、src/App.vueの「script」にimportさせる。<br>
→　さらに、同じくsrc/App.vueの「template」に＜TestComponent/＞を追加する。

```javascript
/** src/App.vue */
<script>
import HelloWorld from './components/HelloWorld.vue'
import TestComponent from './components/TestComponent.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    TestComponent //←　こいつを追加しないとエラーになる
  }
}
</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <TestComponent />
</template>
```


→　次に親コンポーネントからデータを渡せるようにする。<br>
→　コンポーネントからデータを渡すためには、**Props**を使う。<br>
→　App.vueから、TestComponent.vueに、Propsでデータを渡す。<br>


●　ここでやるべきこと

1. 子側(TestComponent.vue)・・・defineProp関数を使って、受け取るPropsの名前と型を定義する。<br>表示するときは｛｛名前｝｝と書く。
2. 親側(App.vue)・・・コンポーネントのタグの属性として、渡したい値を書く。



```html
<!-- src/components/TestComponent.vue -->
<template>
    <p>{{text}}</p>
</template>

<script setup>  //scriptタグにはsetupという指定が必要
import { defineProps } from "vue"     // <a href="#lesson2-note1">※注１</a>　defineProps使うときはimport必要
  defineProps({
    text: String,  //名前：text、型：String
  });
</script>
```


```javascript
/** src/App.vue */
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <TestComponent test="hoge" />
</template>
```


---

<a name="#lesson2-note1">※注１</a>　importが必要な理由

知らずに使うと下記のエラーが発生する。

```
error  'defineProps' is not defined  no-undef
```

ESLintに引っかかってしまうことと、ESLintや下記のプラグインのバージョンによってエラーとなることが多い。

- eslint-plugin-vue
- @vue/eslint-config-typescript


（資料）

Vue3 の SFC (script setup) を TypeScript で使用する時に VSCode の lint エラーを解決する手順

https://qiita.com/soumi/items/d3f45bef08c154a95b5f

<br>  <br>  

--------------------
--------------------
--------------------

<br>  <br>  


<a name="#L3"></a>
<br><br>

# 【Vue.js入門#3】Vue.jsでWebアプリケーションを作ろう！/データバインディング【Vue3】

https://www.youtube.com/watch?v=9S14LADnfX8&list=PL33OZZ24O4xDJ-_mqltklx8-9DK79iDOj&index=3


## Vurのデータ

親から渡す以外にも、Vueのデータを持つことができる。

&lt;script setup&gt;&lt;/script&gt;内で、通常のJavaScriptを組み込むことで実現。

→　前回の`src/components/TestComponent.vue`に、ソースコードを追加する。

→　この時、見づらさを解消するためApp.vueは、&lt;TestConponent /&gt;以外はすべてコメントアウトする。（プロパティなどの関連記述もコメントアウトする。）

```javascript

/* src/components/TestComponent.vue */
<template>
    <p>{{dataSet}}</p>  // ←　変更
</template>

<script setup>
import { defineProps } from "vue" 

defineProps({
    text: String
})

const dataSet = "これはデータです。";

</script>

```


## データバインディング

HTML要素とVueのデータを結び付ける機能。

1. テキストバインディング
2. 属性バインディング
3. イベントバインディング
4. 双方向バインディング


### 1. テキストバインディング

HTML内にテキストとしてデータ表示させる。

#### ①　mustache構文を使う

```html
<template>
    <p>{{ hoge }}</p>
</template>
```


#### ①　v-textを使う

```html
<template>
    <p v-text="hoge"></p>
</template>
```

①と②とも、結果は同じになる。（Vue3は`mustache構文`が一般的）

---

### 2. 属性バインディング

HTML要素の属性に、データを割り当てる。
`v-bind:属性名='データの名前'`とかく。

```html
<template>
    <img v-bind:src="imageUrl" />
    <img :src="imageUrl" />  <!--省略例-->
</template>

<script setup>
const imageUrl = "./sample.png";
</script>

```

---

### 3. イベントバインディング

HTML要素のイベント(clickなど)と、Vueのメソッドと結びつける。

`v-on:イベントの種類='メソッド名'`とかく。


```javascript

<template>
    <button v-on:click="myMethod">メソッド実行</button>
    <button @click="myMethod">メソッド実行</button>     // ← 省略記法
</template>

<script setup>

function myMethod(){
    console.log('メソッド実行');
}
</script>

```

---

### 4. 双方向バインディング(two-way data binding)

HTMLフォーム要素と、データを双方向に結びつける。

片方が変わったら、もう片方にも反映させる。

- &lt;imput&gt;要素に、`v-model='データの名前'`と書く。
- データの宣言は、`ref関数`を使用し、`const データの名前=ref('初期値')`と書く。

##### 　→　ref関数とは

```

ref関数で値を宣言・・・その値を常に監視し、データが変更されるとすぐに画面に反映されるようになる。
v-modelとセットで使用される。

```


```javascript

<template>
    <div>
      <label for="name">名前：</label>
      <input type="text" id="name" v-model="name">
      <p>入力された名前：{{ name }}</p>
    </div>
</template>

<script setup>
import { ref } from "vue" 
const name = ref('');
</script>

```


---

## 結び

Lesson3で使用された`v-〇〇`は、`ディレクティブ`と呼ばれる




