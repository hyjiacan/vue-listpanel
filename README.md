# ListPanel

A list panel component for Vue.js 2.0

### Dependencies
- Vue.js 2.x
- Less

## Install

```bash
npm i @hyjiacan/vue-listpanel
```

or

```bash
yarn add @hyjiacan/vue-listpanel
```

For the latest code, you can:

```bash
git clone https://github.com/hyjiacan/vue-listpanel.git
```
or [download archive](https://github.com/hyjiacan/vue-listpanel/archive/master.zip)

## Usage

### Global (recommend)

*main.js*
```javascript
import Vue from 'vue'
import ListPanel from '@hyjiacan/vue-listpanel'
import '@hyjiacan/vue-listpanel/lib/listpanel.css'

// import ListPanel component, and set the defaults props
Vue.use(ListPanel, {
  // set props here
})
```

### In Component

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

For more usage, see https://hyjiacan.github.io/vue-listpanel/

## ListPanel Properties

#### title (optional)

- type `String`

> Title text, if this property and the slot `header` are empty, header would be hidden

#### collapsed (optional)

- type `Boolean`
- default `false`

> Whether to collapse panel content

#### showCollapse (optional)

- type `Boolean`
- default `true`

> Is the collapse button visible

#### collapseFooter (optional)

- type `Boolean`
- default `false`

> Whether to hide `footer` while collapsed

#### showHeader (optional)

- type `Boolean'
- default `true`

> Is the header visible

#### multi (optional)

- type `Boolean'
- default `false`

> Whether to enable multi-selection

#### selected (optional)

- type `String/Number/Array/Object'

> Specify the selected items, modifier `.sync` is available

#### customClass (optional)

- type `String'

> Customize class name

#### readonly (optional)

- type `Boolean'
- default `false`

> Is list `readonly`, if `true`, cannot toggle selected by mouse-click

#### inline (optional)

- type `Boolean'
- default `false`

> Whether to make it in `inline` mode （Display multiple items in one line）

#### equal (optional)

- type `Function'

> Is two value equals，useful while the `value` property is `Object`


## ListPanel Slots

#### default (required)

> List items

#### header (optional)

> The header content，property `title` would be ignored

#### footer (optional)

> Footer content

## PanelList Events

#### change

- args While `multi=true`: `[selected]`，item is a selected value; otherwise `selected`

### PanelListItem Properties

#### value (optional)

- type `String/Number/Object/`

> The value of this item

#### selected (optional)

- type `Boolean`
- default `false`

> Is this item selected

#### ignoreClick (optional)

- type `Boolean`
- default `false`

> Whether to ignore click event on this item

### PanelListItem Slots

#### default (required)

- args `{selected, value}`, `selected` is this item selected，`value` the value of this item

> Contents of this item 

## Development

```bash
yarn
# start dev server
yarn serve
# Build library
yarn release
```
