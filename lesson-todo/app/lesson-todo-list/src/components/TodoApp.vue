<template>
  <div class="todoApp">
    <TodoInput></TodoInput>
    <TodoListView></TodoListView>
  </div>
</template>

<script setup>
import TodoInput from './TodoInput.vue'
import TodoListView from './TodoListView.vue'

</script>

<style scoped>
.todoApp > * {
  margin: 2rem 0 0 0;
}
</style>