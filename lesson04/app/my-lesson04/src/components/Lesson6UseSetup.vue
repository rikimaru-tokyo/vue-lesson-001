<template>
    <h3>## Lesson6-2: setupを使う場合</h3>
    <div>
        <p>{{ count }}</p>
        <button @click="incrementCount">incrementCount</button>        
    </div>
</template>


<script setup>
    import { 
        ref, 
        onBeforeMount, 
        onMounted,
        onBeforeUpdate,
        onUpdated,
        onBeforeUnmount,
        onUnmounted,
    } from 'vue';

    const count=ref(0);
    const incrementCount=()=>{
        count.value++;
    };

    console.log("beforeCreate: コンポーネントが作成される直前に呼び出される");
    console.log("created: コンポーネントが作成された直後に呼び出される");
    onBeforeMount(()=>{
        console.log("onBeforeMount:コンポーネントがDOMに取り付けられる直前に呼び出される");
    });
    onMounted(()=>{
        console.log("onMounted:コンポーネントがDOMに取り付けられた直後に呼び出される");
    });
    onBeforeUpdate(()=>{
        console.log("onBeforeUpdate:コンポーネントが再描画される直前に呼び出される");
    });
    onUpdated(()=>{
        console.log("onUpdated:コンポーネントが再描画された直後に呼び出される");
    });
    onBeforeUnmount(()=>{
        console.log("onBeforeUnmount:コンポーネントがDOMから除去される直前に呼び出される");
    });
    onUnmounted(()=>{
        console.log("onUnmounted:コンポーネントがDOMから除去された直後に呼び出される");
    });

</script>