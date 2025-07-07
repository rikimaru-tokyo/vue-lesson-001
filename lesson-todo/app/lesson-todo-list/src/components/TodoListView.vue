<template>
    <p v-if="isErrorMsg">{{ errMsg }}</p>
    <div>
        <table>
            <tr class="title">
                <th class="th-id">ID&nbsp;<button @click="sortById()">↓</button></th>
                <th class="th-value">やること</th>
                <th class="th-limit">期限&nbsp;<button @click="sortByLimit()">↓</button></th>
                <th class="th-state">状態</th>
                <th class="th-edit">編集</th>
                <th class="th-delete">削除</th>            
            </tr>
            <tr v-for="item in items" :key="item.id" :class="{red: new Date(item.limit) < today}">
                <td>{{ item.id }}</td>
                <td>
                    <span v-if="!item.onEdit" >{{ item.content }}</span>
                    <input v-else v-model="inputContent" type="text" />
                </td>
                <td>
                    <span v-if="!item.onEdit">{{ item.limit }}</span>
                    <input v-else v-model="inputLimit" type="date" />
                </td>
                <td>
                    <span v-if="!item.onEdit" >{{ item.state.value }}</span>
                    <select v-else v-model="inputStatus">
                        <option v-for="state in statuses" :key="state.id" :value="state" :selected="state.id == item.state.id">
                        {{ state.value }}
                        </option>
                    </select>
                </td>
                <td>
                    <button class="btn" v-if="!item.onEdit" @click="onEdit(item.id)">編集</button>
                    <button class="btn" v-else @click="onUpdate(item.id)">完了</button>
                </td>
                <td><button class="btn" @click="showDeleteModal(item.id)">削除</button></td>            
            </tr>
        </table>
    </div>

    <div v-if="isShowModal" class="modal">
        <div class="modal-content"> 
        <p>タスク:{{ deleteItemContent }} を削除してもよいですか？</p>
            <button @click="onDeleteItem">はい</button> &nbsp; &nbsp;
            <button @click="onHideModal">キャンセル</button> 
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue';
    import { statuses } from '@/const/common';
    let items = ref(JSON.parse(localStorage.getItem("items")) || []);
    let inputContent = ref();
    let inputLimit = ref();
    let inputStatus = ref();
    const isErrorMsg = ref(false);
    let isShowModal = ref(false);
    let deleteItemId = '';
    let deleteItemContent = ref();
    let isOnEditOther = false;
    let errMsg = ref();

    const today = new Date();

    function onEdit(id){
        items.value.map((item)=>{
            if (item.onEdit){
                isOnEditOther = true;
                return;
            }
        });

        if(isOnEditOther){
            errMsg = 'ほかに編集中のタスクがあります';
            isErrorMsg.value = true;
            return false;
        }

        inputContent.value = items.value[id].content;
        inputLimit.value = items.value[id].limit;
        inputStatus.value = items.value[id].state;
        items.value[id].onEdit = true;
    }

    function onUpdate(id){
        if(inputContent.value=='' || inputLimit.value==''){
            errMsg = 'タスク・期限を両方入力してください';
            isErrorMsg.value = true;
            return false;
        }

        const newItem = {
            id: id,
            content: inputContent.value,
            limit: inputLimit.value,
            state: inputStatus.value,
            onEdit: false,
        };

        //↓ 用例：array.splice(start, deleteCount, item1, item2, ...);
        items.value.splice(id, 1, newItem);
        
        //更新後のitemsを配列全体ごと置き換える
        localStorage.setItem("items",  JSON.stringify(items.value));

        isErrorMsg.value = false;
    }

    function showDeleteModal(id){
        isShowModal.value = true;
        deleteItemId = id;
        deleteItemContent = items.value[id].content;
    }

    function onDeleteItem(){
        //配列要素削除
        items.value.splice(deleteItemId, 1);

        //IDを全面的に振りなおす
        items.value = items.value.map((item, index)=>({
            id: index,
            content: item.content,
            limit: item.limit,
            state: item.state,
            onEdit: item.onEdit,
        }));

        localStorage.setItem("items",  JSON.stringify(items.value));

        isShowModal.value=false;
    }

    function onHideModal(){
        isShowModal.value=false;
    }

    function sortByLimit(){
        items.value.sort((a , b) => new Date(a.limit) - new Date(b.limit));
        localStorage.setItem("items", JSON.stringify(items.value));
    }

    function sortById(){
        items.value.sort((a , b) => a.id - b.limit);
        localStorage.setItem("items", JSON.stringify(items.value));
    }

</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
}

.red {
  color: red;
}
table > * > th {
  width: 16.666%;
}
table {
  width: 100%;
}
.btn {
  width: 100%;
}
button {
  border: none;
  border-radius: 5px;
}
.title {
  background-color: rgb(158, 212, 158);
}
</style>
