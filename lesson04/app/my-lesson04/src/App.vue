<template>
  <!--img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/ -->
  <Lesson_4_Component />
  <!-- Junk_Test_Component name="hoge"/ -->

<Lesson6NotUseSetupComponent />

<Lesson6UseSetupComponent />

</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Lesson_4_Component from './components/Lesson4Component.vue'
//import Junk_Test_Component from './components/JunkTest001.vue'
import Lesson6NotUseSetupComponent from './components/Lesson6NotUseSetup.vue'
import Lesson6UseSetupComponent from './components/Lesson6UseSetup.vue'


export default {
  name: 'App',
  components: {
//    HelloWorld
         Lesson_4_Component,
//         Junk_Test_Component,
       Lesson6NotUseSetupComponent,
       Lesson6UseSetupComponent,
  }
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
