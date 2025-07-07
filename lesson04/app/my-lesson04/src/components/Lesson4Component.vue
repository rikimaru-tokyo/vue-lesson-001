<template>

<h3> ##Lesson 4-1 </h3>

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
<!-- :key="key"は、キー変数に「key」と命名するという意味になる。
 ハッシュが使われる場合は、:key="key.id"などでキー名を指定する。
 フォーム要素を追加・更新・削除するときには、:key="key"で明示しておかないと、思わぬ挙動を引き起こす。 -->


<h3> ##Lesson 4-2 </h3>

ナンバー：{{ number }}

<p v-if="number >= 10"> 10以上</p>
<p v-else> 10未満</p>



<h3> ##Lesson 4-3 </h3>

ナンバー：{{ number }}

<p v-show="number >= 10"> 10以上</p>

</template>


<script setup>

// ##Lesson 4-1
const fruitList=['りんご','いちご','バナナ'];

// ##Lesson 4-2,4-3
const number = 5;

</script>

