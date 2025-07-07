<template>
  <div>
    <p v-if="isErrorMsg">タスク・期限を両方入力してください。</p>
    <!-- form @submit.prevent="onSubmitForm"-->
    <form @submit="onSubmitForm">
      <label>やること<input type="text" v-model="input" /></label><br />
      <label>期限<input type="date" v-model="inputDate" /></label><br />
      <input class="submit" type="submit" value="登録！" />
    </form>
  </div>
</template>

<script setup>
    import { ref } from 'vue';
    import { statuses } from '@/const/common';

    const input = ref('');
    const inputDate = ref('');
    const isErrorMsg = ref(false);

    function onSubmitForm(){

        //バリデーション
        if(input.value == '' || inputDate.value == '' ) {
            isErrorMsg.value = true
            event.preventDefault();
            return false;
        }

        // 1. 現在のデータをローカルストレージから取得
        
        const items = JSON.parse(localStorage.getItem("items")) || [];
        const newItem = {
            id: items.length,
            content: input.value,
            limit: inputDate.value,
            state: statuses.NOT_START,
            onEdit: false,
        };

        // 2. 新しいタスクをデータにpushする
        items.push(newItem);
        // 3. タスクを追加したデータをローカルストレージに保存 
        localStorage.setItem('items', JSON.stringify(items));
    }

</script>

<style scoped>
input {
  width: 70%;
}
label {
  display: flex;
  justify-content: space-between;
}
.submit {
  width: 100%;
}
</style>