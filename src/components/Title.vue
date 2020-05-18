// 段落的标题
<template>
  <div>
    <h2 class="text">
      <a :href="href">{{text}}</a>
    </h2>
    <hr v-if="hasHr">
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

@Component
export default class Title extends Vue {
  @Prop({required: true, default: ''}) private text?: string
  @Prop({default: ''}) private href?: string
  @Prop({default: true}) private hasHr?: string

  private github: object = require('@/assets/images/github.svg')
}
</script>

<style lang="stylus">
.text
  font-size 1.5rem
  margin 0
a:hover
  text-decoration underline
hr
  margin 0
</style>
 