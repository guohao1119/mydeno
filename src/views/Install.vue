<template>
  <div class="main">
    <h1>Deno</h1>
    <h2>
      JavaScript和TypeScript的安全运行时。
    </h2>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import MyTitle from '@/components/Title.vue';

// 导航栏项目
interface NavItem {
  label: string,
  href?: string
}

@Component({
  components: {
    MyTitle
  }
})
export default class Header extends Vue {
  private title: string = 'Deno 1.0'
  private date: string = '2020--5-13'
  private author: string = 'Ryan Dahl, Bert Belder, and Bartek Iwańczuk'
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

<style lang="stylus">
</style>
 