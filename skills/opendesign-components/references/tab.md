# OTab / OTabPane

标签页组件，用于在不同内容区域之间切换。

## OTab Props

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `modelValue` | `string \| number` | — | 当前激活的 tab 值（v-model） |
| `variant` | `'solid' \| 'text' \| 'button'` | `'text'` | 标签页样式 |
| `size` | `'small' \| 'medium' \| 'large'` | — | 尺寸 |
| `round` | `string` | — | 圆角值（`button` 模式下有效） |
| `lazy` | `boolean` | `false` | 懒加载，首次展示时才渲染 |
| `addable` | `boolean` | `false` | 是否显示添加按钮（可新增标签） |
| `maxShow` | `number` | — | 最多显示的标签数，超出折叠 |
| `line` | `boolean` | `true` | 是否显示标签栏底部线 |
| `headerClass` | `string \| Array \| Object` | — | 标签头部自定义类名 |

## OTabPane Props

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `value` | `string \| number` | — | 标识值，与 OTab 的 modelValue 对应 |
| `label` | `string` | — | 标签文本 |
| `disabled` | `boolean` | `false` | 禁用该标签 |
| `closable` | `boolean` | `false` | 是否显示关闭按钮 |
| `lazy` | `boolean` | `false` | 懒加载（覆盖 OTab 的 lazy 设置） |
| `unmountOnHide` | `boolean` | `false` | 隐藏时是否卸载内容（节省内存） |

## OTab 插槽

| 插槽 | 说明 |
|------|------|
| `prefix` | 标签头部前置内容 |
| `suffix` | 标签头部后置内容 |

## OTabPane 插槽

| 插槽 | 说明 |
|------|------|
| `default` | 标签页内容 |
| `label` | 自定义标签文本 |

## OTab 事件

| 事件 | 类型 | 说明 |
|------|------|------|
| `change` | `(value, oldValue) => void` | 切换 tab 时触发 |
| `delete` | `(value) => void` | 点击关闭按钮时触发（需配合 `closable`） |
| `add` | `(evt: MouseEvent) => void` | 点击添加按钮时触发（需配合 `addable`） |

## 示例代码

```vue
<template>
  <!-- 基础用法（text 样式） -->
  <OTab v-model="activeTab">
    <OTabPane value="tab1" label="标签1">
      <div>标签1的内容</div>
    </OTabPane>
    <OTabPane value="tab2" label="标签2">
      <div>标签2的内容</div>
    </OTabPane>
    <OTabPane value="tab3" label="标签3" disabled>
      <div>禁用标签的内容</div>
    </OTabPane>
  </OTab>

  <!-- 按钮样式 -->
  <OTab v-model="activeTab" variant="button" round="pill">
    <OTabPane value="list" label="列表" />
    <OTabPane value="grid" label="网格" />
  </OTab>

  <!-- 可关闭标签（动态管理） -->
  <OTab v-model="activeTab" addable @add="handleAdd" @delete="handleDelete">
    <OTabPane
      v-for="tab in tabs"
      :key="tab.value"
      :value="tab.value"
      :label="tab.label"
      closable
    >
      {{ tab.content }}
    </OTabPane>
  </OTab>

  <!-- 自定义标签内容 -->
  <OTab v-model="activeTab">
    <OTabPane value="inbox">
      <template #label>
        收件箱 <OBadge :value="99" />
      </template>
      收件箱内容
    </OTabPane>
  </OTab>

  <!-- 懒加载 -->
  <OTab v-model="activeTab" lazy>
    <OTabPane value="a" label="页面A"><HeavyComponent /></OTabPane>
    <OTabPane value="b" label="页面B"><HeavyComponent /></OTabPane>
  </OTab>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTab, OTabPane, OBadge } from '@opensig/opendesign'

const activeTab = ref('tab1')

const tabs = ref([
  { value: 'tab1', label: '标签1', content: '内容1' },
  { value: 'tab2', label: '标签2', content: '内容2' },
])

let tabIndex = tabs.value.length

const handleAdd = () => {
  tabIndex++
  const newTab = { value: `tab${tabIndex}`, label: `标签${tabIndex}`, content: `内容${tabIndex}` }
  tabs.value.push(newTab)
  activeTab.value = newTab.value
}

const handleDelete = (value: string | number) => {
  const idx = tabs.value.findIndex(t => t.value === value)
  if (idx !== -1) tabs.value.splice(idx, 1)
  if (activeTab.value === value && tabs.value.length > 0) {
    activeTab.value = tabs.value[Math.max(0, idx - 1)].value
  }
}
</script>
```

## 导入方式

```vue
<script setup>
import { OTab, OTabPane } from '@opensig/opendesign';
</script>
```
