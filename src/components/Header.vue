<template>
  <div>
    <nav>
      <img class="logo" alt="Vue logo" :src="logo">
      <div class="title">{{title}}</div>

      <div class="nav-item" v-for="item in navList" :key="item.id">
        <a :href="item.href">{{ item.label }}</a>
      </div>
      <img class="github" :src="github" alt="git">
    </nav>
    <div class="div-img">
      <img :src="deno" alt="deno">
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

// 导航栏项目
interface NavItem {
  label: string,
  href?: string
}

@Component
export default class Header extends Vue {
  private logo: object = require('@/assets/images/logo.svg')
  private github: object = require('@/assets/images/github.svg')
  private deno: object = require('@/assets/images/deno.jpg')
  private title: string = 'Deno'
  private navList!: NavItem[]

  private created() {
    this.navList = [
      { label: '安装', href: '' },
      { label: '手册', href: '' },
      { label: '标准库', href: '' },
      { label: '第三方模块', href: '' },
    ]
  }
}
</script>

<style lang="stylus" scoped>
.logo
  width 3rem
  height 3rem
.title
  margin-left 1.5rem
  font-size 24px
  font-weight bold
nav
  display flex
  justify-content center
  align-items center
  flex-direction row
  padding 1.5rem 0
  .nav-item {
    margin-left 2.5rem 
  }
.github
  width 30px
  margin-left 2.5rem
.div-img
  width 100%
  background-color rgb(47, 46, 44)
  img
    width 100%
    max-width 1024px
</style>
 