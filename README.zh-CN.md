# ListPanel

一个 Vue.js 2.0 的可选择列表面板

### 依赖
- Vue.js 2.x
- Less

## 安装

```bash
npm i @hyjiacan/vue-listpanel
```

或

```bash
yarn add @hyjiacan/vue-listpanel
```

可以通过以下方式获取最新代码:

```bash
git clone https://github.com/hyjiacan/vue-listpanel.git
```
或 [下载归档](https://github.com/hyjiacan/vue-listpanel/archive/master.zip)

## 使用

### 全局引用 (推荐)

*main.js*
```javascript
import Vue from 'vue'
import ListPanel from '@hyjiacan/vue-listpanel'
import '@hyjiacan/vue-listpanel/lib/listpanel.css'

// 引入 ListPanel 组件，并设置组件默认值
Vue.use(ListPanel, {
  // 在此处填写默认的属性值
})
```

### 组件内引用

*Foobar.vue*
```html
<list-panel :selected="[]">
    <list-panel-item :value="1">Content</list-panel-item>
    <list-panel-item :value="1">
        <template v-slot="{value, selected}">
           value: {{value}}, selected: {{selected}}
        </template>
    </list-panel-item>
</list-panel>
<script>
import ListPanel from '@hyjiacan/vue-listpanel'
import '@hyjiacan/vue-listpanel/lib/listpanel.css'

export default {
    name: 'Foobar',
    components: {ListPanel}
}
</script>
```

更多的用法，参见 https://hyjiacan.github.io/vue-listpanel/

## ListPanel 属性

#### title (可选)

- 类型 `String`

> 标题文本，如果此属性为空，`slot=header` 也为空,那么头部会被隐藏

#### collapsed (可选)

- 类型 `Boolean`
- 默认值 `false`

> 设置是否收起内容

#### showCollapse (可选)

- 类型 `Boolean`
- 默认值 `true`

> 是否显示收起按钮

#### collapseFooter (可选)

- 类型 `Boolean`
- 默认值 `false`

> 在收起时，是否同时收起 footer 部分

#### showHeader (可选)

- 类型 `Boolean'
- 默认值 `true`

> 是否显示头部

#### multi (可选)

- 类型 `Boolean'
- 默认值 `false`

> 设置是否多选

#### selected (可选)

- 类型 `String/Number/Array/Object'

> 设置选中项，支持使用 `.sync` 修饰

#### customClass (可选)

- 类型 `String'

> 自定义样式

#### readonly (可选)

- 类型 `Boolean'
- 默认值 `false`

> 是否只读，在只读时不能通过鼠标点击设置项的选中状态

#### inline (可选)

- 类型 `Boolean'
- 默认值 `false`

> 内容是否行内显示（一行可以显示多个项）

#### equal (可选)

- 类型 `Function'

> 判断项是否相等，在值为对象时使用


## ListPanel 插槽

#### default (必填)

> 内容为列表项

#### header (可选)

> 头部内容，指定时，设置的`title`无效

#### footer (可选)

> 底部内容

## PanelList 事件

#### change

- 参数 在多选(`multi=true`)时为`[selected]`，项为一个选中项的值；在单选时为`selected`

### PanelListItem 属性

#### value (可选)

- 类型 `String/Number/Object/`

> 此项的值，在此项可用时应该始终指定此属性

#### selected (可选)

- 类型 `Boolean`
- 默认值 `false`

> 此项的选中状态

#### ignoreClick (可选)

- 类型 `Boolean`
- 默认值 `false`

> 是否忽略此项的点击事件

### PanelListItem 插槽

#### default (必填)

- 参数 `{selected, value}`, `selected` 指示当前项是否选中，`value`是当前项的值

> 列表项的内容

## 开发

```bash
yarn
# 启动服务器
yarn serve
# 构建仓库
yarn release
```
