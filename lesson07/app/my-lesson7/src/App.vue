<template>
  <h3>## Lesson7</h3>
  <Lesson7Component @message="handleMessage"></Lesson7Component>
  <p>{{ receivedMessage }}</p>
<hr>

</template>

<script>
import Lesson7Component from './components/Lesson7Component.vue'


export default {
  name: 'App',
  components: {
    Lesson7Component,
  },
  data(){
    return {
      receivedMessage:"",   //Lesson7
    };
  },
  methods: {
    //Lesson7
    handleMessage(message){
                  //↑ 子コンポーネントから受け取ったデータ
      this.receivedMessage = message;
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
