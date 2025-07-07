# Vue.js入門 Lesson4～6

～目次～

- <a href="#L4">Lesson4</a>
- <a href="#L5">Lesson5</a>
- <a href="#L6">Lesson6</a>

---
<a name="#L4"></a>
<br><br>

# 【Vue.js入門#4】Vue.jsでWebアプリケーションを作ろう！/ディレクティブ【Vue3】

https://www.youtube.com/watch?v=60w_Vn1zezo&list=PL33OZZ24O4xDJ-_mqltklx8-9DK79iDOj&index=4

<br><br>  

## ディレクティブとは？

Vue.jsで使われる特別な属性のこと。HTML要素の属性として使用し、その要素の表示や挙動を制御する。

`v-model`の様に、`v-〇〇`という形式で定義される。


### v-for

リスト（配列）のデータをループ表示できるディレクティブ。


<del>記法： v-for='変数名 in 配列名'</del>

記法： <span style="color: #66FF66;"> v-for='(value変数名, key変数名) in 配列名' :key=""</span> <a href="#L4-01">(※注１)</a>

```html
<p>配列べた書きパターン</p>
<ul>
    <li>{{ fruitList[0] }}</li>
    <li>{{ fruitList[1] }}</li>
    <li>{{ fruitList[2] }}</li>
</ul>

<p>v-forを使ったパターン</p>
<ul>
    <li v-for="(value,key) in fruitList" :key="key">{{ key }} ： {{ value }}</li>
</ul>

<script setup>
const fruitList=['りんご','いちご','バナナ'];
</script>
```


<a name="#L4-01">(※注１)</a>


**(value変数名, key変数名)** を指定しないと、ESLintでエラーになる。


```shell
error  Elements in iteration expect to have 'v-bind:key' directives  vue/require-v-for-key
```

●　[備忘録] vuejs エラー Elements in iteration expect to have　'v-bind:key' directives

https://qiita.com/MakiMatsu/items/ef2eadbce13dc227d3bd


---

### v-if、v-else

条件を使用して、要素の表示・非表示を切り替えられるディレクティブ。

記法：<span style="color: #66FF66;">v-if="条件"</span>で、条件が`true`の場合にその要素は表示される。<br>
　　　`v-if`のある直後の要素で、<span style="color: #66FF66;">v-else</span>を使うと、`v-if`の条件に当てはまらない場合に、`v-else`の要素が表示される。


```html
<template>
ナンバー：{{ number }}

<p v-if="number >= 10"> 10以上</p>
<p v-else> 10未満</p>
</template>

<script setup>
const number = 5;
</script>
```


---

### v-show

`v-if`に似たディレクティブに、<span style="color: #66FF66;">v-show</span>がある。<br>
（`v-else`を必要としない）<br>
ただし、CSSの`display:none;`で隠しているだけなので注意する。

```
v-ifは非表示になるときに要素が削除されるため、再表示するためにかかるコストが、v-showと比べて大きい。
そのため、条件が頻繁に切り替わる場合は、v-showのほうが良い。
```


記法：<span style="color: #66FF66;">v-show="条件"</span>

```html
<template>
ナンバー：{{ number }}

<p v-show="number >= 10"> 10以上</p>
</template>

<script setup>
const number = 5;
</script>
```




--------------------
--------------------
--------------------

<br><br>

<a name="#L5"></a>
<br><br>

# 【Vue.js入門#5】Vue.jsでWebアプリケーションを作ろう！/setup【Vue3】

https://www.youtube.com/watch?v=bsS8FID3PqQ&list=PL33OZZ24O4xDJ-_mqltklx8-9DK79iDOj&index=5&t=2s

<br><br> 


## setup()関数とは？

コンポーネントのロジックを定義するための特別な関数。

コンポーネントの中で、データやメソッドを定義するために使う。

setup()関数を使うことで、普通のJavaScriptのようにデータやメソッドを定義できる。

（Vue2では、コンポーネント内でデータやメソッドを定義するには、専用のオプションを使用する必要があった）

●　Vue2の時

```javascript
<script>
export default {
    data() {
        return {
            message: "テキスト",
        };
    },
    methods: {
        updateMessage() {
            this.message ="新しいメッセージ"；
        },
    },
}
</script>
```


●　Vue3では

```javascript
<script setup>
const message = ref("テキスト");
const updateMessage = () => {
    message ="新しいメッセージ"；
};
</script>
```



## setupの使い方

`<script setup>`と書くことで、`setup`関数を使うことになる。

その中で、通常のJavaScriptのようにデータやメソッドを定義することができる。

データの定義には`ref()関数`を使用してリアクティブなデータを宣言できる。


### （Qiita抜粋）refってなに

```
refとは一言で表すと、「Vue3でリアクティブな変数を定義する時に使うやつ」です。

厳密には、Vue3のComposition APIという記法の中で使われている一要素でリアクティブな値の実現させている機能です。

一応リアクティブとは何かというのも説明しておくと、
「値が監視されていて、その値が更新された時に変更が検知される状態のこと」です。

値の変更を監視することで、値が変更した瞬間リアルタイムで処理を走らせ画面に反映させたりします。
```


●　参考：Vue3で出てくるrefの使い方(reactiveも)

https://qiita.com/Yuto_Tatsumi/items/25e46a9e6576843d470c

---

### (注意) `<script>`タグの中に書かず、`setup()関数`として定義する方法もあるが、冗長になるため推奨されない。

●　ソース例

```javascript

<script>
import { ref } from 'vue';

export default {
    setup() {
        const count = ref(0);      // ┐ もし<script setup>のタグ
        const increment = () => {　// │ の中だけで書く場合は
            count.value++;　       // │ これらのコードだけで収まる
        };                         // ┘

        return {
            count,
            increment,
        };
    },
};
</script>
```


--------------------
--------------------
--------------------

<br><br>

<a name="#L6"></a>
<br><br>

# 【Vue.js入門#6】Vue.jsでWebアプリケーションを作ろう！/ライフサイクルフック【Vue3】

https://www.youtube.com/watch?v=H8sQAO2Gn7c&list=PL33OZZ24O4xDJ-_mqltklx8-9DK79iDOj&index=6


## ライフサイクルフックとは

コンポーネントの一生（ライフ）に関連する特別な関数。

- 作成
- 更新
- 削除 etc.

それぞれのステップでコード実行する。

ライフサイクルフックを使うとコンポーネントがどの段階にあるのかを把握でき、必要な処理を行うことができる。



## ライフサイクルフックの種類

|ライフサイクルフック名|詳細|
|:-----:|:-----:|
|beforeCreate|コンポーネントが作成される直前に呼び出される|
|created|コンポーネントが作成された直後に呼び出される|
|beforeMount|コンポーネントがDOMに取り付けられる直前に呼び出される|
|mounted|コンポーネントがDOMに取り付けられた直後に呼び出される|
|beforeUpdate|コンポーネントが再描画される直前に呼び出される|
|updated|コンポーネントが再描画された直後に呼び出される|
|beforeUnmount|コンポーネントがDOMから除去される直前に呼び出される|
|unmounted|コンポーネントがDOMから除去された直後に呼び出される|


用途：

- データ初期化
- 非同期リクエスト実行　→　`created`
- DOMへのアクセス、外部ライブラリの初期化 　→　`mounted`



### (Vue.jsドキュメントより) OptionsAPI一覧

https://ja.vuejs.org/api/options-lifecycle


1. beforeCreate
1. created
1. beforeMount
1. mounted
1. beforeUpdate
1. updated       (※注１)
1. beforeUnmount
1. unmounted
1. errorCaptured
1. renderTracked <span style="color:#ffe600;">(※Devのみ)</span>
1. renderTriggered <span style="color:#ffe600;">(※Devのみ)</span>
1. activated
1. deactivated
1. serverPrefetch <span style="color:#ffe600;">(※SSRのみ)</span>

> [!WARNING]
> 
> (※注１)
> 
> 更新フックでコンポーネントの状態を変更しないでください - 無限更新ループになる可能性があります！

---

### (Zenn抜粋) vue.jsのライフサイクルフックについて調べてみた

https://zenn.dev/actbe_tech/articles/002d755efa93b0


|タイミング|Options API|Composition API|
|:-------:|:---------:|:-------------:|
|作成前|beforeCreate()|なし(setup前)|
|作成後|created()|なし(setupで完了)|
|マウント前|beforeMount()|onBeforeMount()|
|マウント後|mounted()|onMounted()|
|更新前|beforeUpdate()|onBeforeUpdate()|
|更新後|updated()|onUpdated()|
|アンマウント前|beforeUnmount()|onBeforeUnmount()|
|アンマウント後|unmounted()|onUnmounted()|
|エラーキャッチ|errorCaptured()|onErrorCaptured()|

---

## コード実例

### setupを使わない場合

```javascript

created(){
    console.log("createdフック：コンポーネントが初期化されました");
},

```

### setupを使う場合

```javascript
console.log("beforeCreateフック：コンポーネントが作成される直前");
console.log("createdフック：コンポーネントが作成された直後");
//↑　<script>直下にそのまま書くこと　↑

onBeforeMount(()=>{
    console.log("BeforeMountフック：コンポーネントがDOMに取り付けられる直前");
});
//↑　ライフサイクル名の直前に「on」をつけ、ライフサイクル名の最初の①文字を大文字にし、その中（アロー関数）に処理を書く。　↑

```



> [!WARNING]
> 
> (※注２)
> 
> ライフサイクルフックは、`import`する必要がある。

```javascript

<script setup>

import { ref, onBeforeMount, onMounted, onBeforeMUpdate, onUpdated } from 'vue';

</script>

```

---


## コード演習




