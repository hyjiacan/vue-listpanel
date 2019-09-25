<template>
  <div class="list-panel-item" :class="{'list-panel-item-selected': isSelected}" @click="itemClick">
    <slot :selected="isSelected" :value="value"></slot>
  </div>
</template>

<script>
export default {
  name: 'ListPanelItem',
  props: {
    // 此项的值
    value: {
      type: [String, Number, Object]
    },
    // 此项的选中状态
    selected: {
      type: Boolean,
      default: false
    },
    // 是否忽略此项的点击事件
    ignoreClick: {
      type: Boolean,
      default: false
    }
  },
  inject: ['event', 'equal'],
  data() {
    return {
      isSelected: false
    }
  },
  mounted() {
    this.isSelected = this.selected
    this.event.$on('value-change', this.onValueChange)
  },
  methods: {
    itemClick() {
      if (this.ignoreClick) {
        return
      }
      this.event.$emit('item-click', this.value)
    },
    onValueChange(values) {
      this.isSelected = !values.every(value => !this.equal(value, this.value))
    }
  },
  beforeDestroy() {
    this.event.$off('value-change', this.onValueChange)
  }
}
</script>
