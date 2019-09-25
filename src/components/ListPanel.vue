<template>
  <div class="list-panel" :class="classes">
    <div class="list-panel-header" v-show="showHeader && (title || $slots.header)">
      <slot name="header">
        <span class="list-panel-header-text">
          {{title}}
        </span>
      </slot>
      <div class="list-panel-header-buttons">
        <slot name="button"></slot>
        <button @click="toggleCollapse" class="list-panel-button-collapse" v-if="showCollapse"></button>
      </div>
    </div>
    <div class="list-panel-body">
      <slot></slot>
    </div>
    <div class="list-panel-footer" v-show="!isCollapsed || !collapseFooter">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  name: 'ListPanel',
  props: {
    // 标题文字
    title: {
      type: String
    },
    // 设置是否收起内容
    collapsed: {
      type: Boolean,
      default: false
    },
    // 是否显示收起按钮
    showCollapse: {
      type: Boolean,
      default: true
    },
    // 在收起时，是否同时收起 footer 部分
    collapseFooter: {
      type: Boolean,
      default: false
    },
    // 是否显示头部
    showHeader: {
      type: Boolean,
      default: true
    },
    // 设置是否多选
    multi: {
      type: Boolean,
      default: false
    },
    // 设置选中项
    selected: {
      type: [String, Number, Array, Object]
    },
    // 自定义样式
    customClass: {
      type: String
    },
    // 是否只读，在只读时不能通过鼠标点击设置项的选中状态
    readonly: {
      type: Boolean,
      default: false
    },
    // 内容是否行内显示（一行可以显示多个项）
    inline: {
      type: Boolean,
      default: false
    },
    // 判断项是否相等，在值为对象时使用
    equal: {
      type: Function,
      default: (a, b) => {
        return a === b
      }
    }
  },
  provide() {
    return {
      event: this.eventBus,
      equal: this.equal
    }
  },
  data() {
    return {
      // 是否折叠
      isCollapsed: false,
      // 选中的数据集合
      selectedSet: [],
      eventBus: new Vue()
    }
  },
  mounted() {
    this.isCollapsed = this.collapsed
    this.eventBus.$on('item-click', this.onItemClick)

    if (this.selected) {
      this.setSelectedItem(this.selected)
    }
  },
  watch: {
    selected(val) {
      this.setSelectedItem(val)
    }
  },
  computed: {
    classes() {
      return {
        'list-panel-collapsed': this.isCollapsed,
        'list-panel-readonly': this.readonly,
        'list-panel-inline': this.inline,
        [this.customClass || '']: true
      }
    }
  },
  methods: {
    setSelectedItem(selected) {
      if (Array.isArray(this.selected)) {
        this.selectedSet = this.selected.slice(0)
      } else {
        this.selectedSet = [this.selected]
      }

      // 触发默认的选中
      this.eventBus.$emit('value-change', this.selectedSet)
    },
    toggleCollapse() {
      this.isCollapsed = !this.isCollapsed
    },
    onItemClick(value) {
      if (this.readonly) {
        // 只读时不响应点击事件
        return
      }
      if (this.multi) {
        // 选择多个
        let idx = this.selectedSet.indexOf(value)

        if (idx === -1) {
          // 如果没有选中，则添加
          this.selectedSet.push(value)
        } else {
          // 如果已经选中，则移除
          this.selectedSet.splice(idx, 1)
        }
      } else {
        // 选中单个
        this.selectedSet = [value]
      }
      this.eventBus.$emit('value-change', this.selectedSet)
      let selected = this.selectedSet.slice(0)
      this.$emit('update:selected', selected)
      this.$emit('change', selected)
    }
  },
  beforeDestroy() {
    this.eventBus.$off('itemClick', this.onItemClick)
    this.eventBus = undefined
    this.selectedSet = undefined
  }
}
</script>

<style lang="less">
@border-color: #cccccc;
.list-panel {
  border: 1px solid @border-color;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
}

.list-panel-button-collapse {
  width: 24px;
  height: 24px;
  text-align: center;
  padding: 0;
  border: none;
  background: none;
  outline: none;

  &:hover {
    border: 1px solid #AAAAAA;
    border-radius: 50%;
  }

  &:after {
    content: '>>';
    transform: rotateX(-180deg) rotateZ(90deg);
    display: inline-block;
    transition: transform 618ms;
  }
}

.list-panel-header {
  padding: 10px 15px;
  border-bottom: 1px solid @border-color;
}

.list-panel-footer {
  &:not(:empty) {
    padding: 10px 15px;
    border-top: 1px solid @border-color;
  }
}

.list-panel-header-buttons {
  float: right;
}

.list-panel-body {
  padding: 10px 15px;

  &:after {
    content: ' ';
    display: block;
    clear: both;
  }
}

.list-panel-collapsed {
  .list-panel-button-collapse {
    &:after {
      transform: rotateX(0deg) rotateZ(90deg);
    }
  }

  .list-panel-header {
    border-bottom: none;
  }

  .list-panel-body {
    display: none;
  }
}

.list-panel-item {
  padding: 5px;
  border-bottom: 1px solid #eeeeee;
  border-left: 3px solid transparent;
  margin: 5px 0;
  transition: border-color 618ms;

  &:hover {
    border-bottom-color: #AAAAAA;
  }
}

.list-panel-item-selected {
  border-left: 3px solid #67839c;
}

.list-panel-inline {
  .list-panel-item {
    float: left;
    margin: 5px;
    border: 1px solid #eeeeee;

    &:hover {
      border-color: #AAAAAA;
    }
  }

  .list-panel-item-selected {
    border-color: darkolivegreen;
  }
}

</style>
