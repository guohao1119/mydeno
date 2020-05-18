<template>
  <div class="footer">
    <nav>
      <div class="nav-item" v-for="item in navList" :key="item.id">
        <a :href="item.href">{{ item.label }}</a>
      </div>
      <img class="github" :src="github" alt="git">
    </nav>
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
export default class Footer extends Vue {
  private github: object = require('@/assets/images/github.svg')
  private navList!: NavItem[]

  private created() {
    this.navList = [
      { label: '运行时文档', href: '' },
      { label: '标准库', href: '' },
      { label: '第三方模块', href: '' },
      { label: '基准测试', href: '' }
    ]
  }
}
</script>

<style lang="stylus" scoped>
.footer
  height 10rem
  border-top 1px solid #d2d6dc
  background-color rgba(249,250,251,0.5)
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
</style>
 