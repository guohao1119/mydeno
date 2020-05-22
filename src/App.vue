<template>
  <div id="app">
    <my-header></my-header>
    <router-view></router-view>
    <!-- <home></home> -->
    <my-footer></my-footer>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import MyHeader from '@/components/Header.vue';
import Home from '@/views/Home.vue';
import MyFooter from '@/components/Footer.vue';

@Component({
  components: {
    HelloWorld,
    MyHeader,
    Home,
    MyFooter
  },
})
export default class App extends Vue {}
</script>

<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
</style>
