<template>
    <button @click="sendMessage">メッセージを送る</button>
</template>

<script>
    export default {
        methods: {
            sendMessage(){
                this.$emit('message', '子コンポーネントから送られたデータ');
            },
        },
    };

//this.$emit('親コンポーネントで受け取るときに使うイベント名', 実際に渡すデータ)
//            ↑ @messageのように使われる。                  ↑複数の引数に渡すこともできる
</script>
