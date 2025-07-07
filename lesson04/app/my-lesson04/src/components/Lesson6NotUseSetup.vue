<template>
    <h3>## Lesson6-1: setupを使わない場合</h3>
    <div>
        <p>{{ count }}</p>
        <button @click="incrementCount">incrementCount</button>        
    </div>
</template>


<script>


export default {
    data(){
        return {
            count :0,
        };
    },
    methods:{
        incrementCount(){
            this.count++;
        },
    },
    beforeCreate() {
        console.log("beforeCreate:コンポーネントが作成される直前に呼び出される");
    },
    created() {
        console.log("created:コンポーネントが作成された直後に呼び出される");
    },
    beforeMount() {
        console.log("beforeMount:コンポーネントがDOMに取り付けられる直前に呼び出される");
    },
    mounted() {
        console.log("mounted:コンポーネントがDOMに取り付けられた直後に呼び出される");
    },
    beforeUpdate() {
        console.log("beforeUpdate:コンポーネントが再描画される直前に呼び出される");
    },
    updated() {
        console.log("updated:コンポーネントが再描画された直後に呼び出される");
    },
    beforeUnmount() {
        console.log("beforeUnmount:コンポーネントがDOMから除去される直前に呼び出される");
    },
    unmounted() {
        console.log("unmounted:コンポーネントがDOMから除去された直後に呼び出される");
    },
}

</script>