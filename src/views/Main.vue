<template>
  <div class="demo-list">
    <list-panel title="单选" :selected="3">
      <list-panel-item v-for="i in 5" :key="i" :value="i">
        <template v-slot="{selected, value}">
          第{{i}}项，值: {{value}}, 是否选中: {{selected}}
        </template>
      </list-panel-item>
    </list-panel>
    <p></p>
    <list-panel title="多选" multi :selected="[2, 4]">
      <list-panel-item v-for="i in 5" :key="i" :value="i">
        <template v-slot="{selected, value}">
          第{{i}}项，值: {{value}}, 是否选中: {{selected}}
        </template>
      </list-panel-item>
    </list-panel>
    <p></p>
    <list-panel title="不显示收起按钮" :selected="{index: {value: 3}}" :equal="isEqual" :show-collapse="false">
      <list-panel-item v-for="i in 5" :key="i" :value="{index: {value: i}}">第{{i}}项</list-panel-item>
    </list-panel>
    <p></p>
    <list-panel title="只读，点击无法设置项的选中状态" :selected="3" readonly>
      <list-panel-item v-for="i in 5" :key="i" :value="i">第{{i}}项</list-panel-item>
      <div slot="footer">
        Footer content
      </div>
    </list-panel>
    <p></p>
    <list-panel title="显示所有内容" :selected="3" collapse-footer>
      <list-panel-item v-for="i in 5" :key="i" :value="i">第{{i}}项</list-panel-item>
      <div slot="footer">
        Footer content
      </div>
    </list-panel>
    <p></p>
    <list-panel title="行内排列项" :selected="3" inline>
      <list-panel-item v-for="i in 50" :key="i" :value="i">第{{i}}项</list-panel-item>
      <div slot="footer">
        Footer content
      </div>
    </list-panel>
  </div>
</template>

<script>
// import {ListPanel, ListPanelItem} from '@/components'

export default {
  name: 'Main',
  // components: {ListPanel, ListPanelItem},
  methods: {
    isEqual(a, b) {
      return a.index.value === b.index.value
    }
  }
}
</script>

<style scoped>
.demo-list{
  padding-bottom: 40px;
}
</style>
