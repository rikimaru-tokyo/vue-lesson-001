<template>
    <p>##Lesson1,2</p>
    <p>{{dataSet}}</p>

    <hr>
    <p>##Lesson3-1: テキストバインディング</p>
    <p v-text="hoge"></p>

    <hr>
    <p>##Lesson3-2: テキストバインディング</p>
    <img v-bind:src="imageUrl" />
    <br>
    <img :src="imageUrl" />  <!--省略例-->

    <hr>
    <p>##Lesson3-3: イベントバインディング</p>
    <button v-on:click="myMethod">メソッド実行</button>
    <br>
    <button @click="myMethod">メソッド実行</button>  <!--省略例-->
    <br>

    <hr>
    <p>##Lesson3-4: 双方向バインディング</p>
    <div>
      <label for="name">名前：</label>
      <input type="text" id="name" v-model="name">
      <p>入力された名前：{{ name }}</p>
    </div>
    <br>

</template>

<script setup>
import { defineProps } from "vue" 
defineProps({
    text: String
})

//##Lesson1,2
const dataSet = "これはデータです。";

//##Lesson3-1
const hoge ="テスト"

//##Lesson3-2
const imageUrl = "icon_001.png";  //publicに画像置いたほうがよさげ

//##Lesson3-3
function myMethod(){
    console.log('メソッド実行');
}

//##Lesson3-4
import { ref } from "vue" 
const name = ref('');

</script>