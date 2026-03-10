# OVirtualList

虚拟滚动列表，高性能渲染大量数据（万级别）。通过只渲染可视区域内的列表项，避免 DOM 数量过多导致的性能问题。

## Props

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `list` | `unknown[]` | — | 数据列表（必需） |
| `itemSize` | `number` | — | 列表项固定高度（px）。已知时设置可大幅提升性能 |
| `defaultItemSize` | `number` | `80` | 未知高度时的估算值（px） |
| `buffer` | `number` | `1` | 缓冲区倍数（相对可视区域的上下额外渲染量，1 = 1倍可视高度） |
| `defaultStartIndex` | `number` | `0` | 初始滚动到的索引位置 |
| `scrollbar` | `boolean \| Object` | `true` | 滚动条配置（`false` 隐藏，对象参数同 OScrollbar） |

## 插槽

| 插槽 | 参数 | 说明 |
|------|------|------|
| `default` | `{ item: any, index: number }` | 列表项模板（必需） |

## 事件

| 事件 | 参数 | 说明 |
|------|------|------|
| `renderChange` | `{ start: number, end: number, visible: number, count: number }` | 渲染范围变化时触发 |

## 暴露方法

| 方法 | 参数 | 说明 |
|------|------|------|
| `scrollToView` | `(index: number, align?: 'start' \| 'center' \| 'end', behavior?: ScrollBehavior)` | 滚动到指定索引的列表项 |

## 示例代码

```vue
<template>
  <!-- 基础用法：固定高度列表项（性能最佳） -->
  <OVirtualList
    :list="bigList"
    :item-size="60"
    style="height: 400px;"
  >
    <template #default="{ item, index }">
      <div class="list-item">
        <span class="index">{{ index + 1 }}</span>
        <span>{{ item.name }}</span>
      </div>
    </template>
  </OVirtualList>

  <!-- 动态高度列表项 -->
  <OVirtualList
    :list="dynamicList"
    :default-item-size="80"
    style="height: 500px;"
  >
    <template #default="{ item }">
      <div class="card">
        <h4>{{ item.title }}</h4>
        <p>{{ item.description }}</p>
      </div>
    </template>
  </OVirtualList>

  <!-- 跳转到指定位置 -->
  <OButton @click="scrollToItem(99)">跳转到第100项</OButton>
  <OVirtualList
    ref="virtualListRef"
    :list="bigList"
    :item-size="60"
    style="height: 400px;"
  >
    <template #default="{ item, index }">
      <div class="list-item">{{ index }}: {{ item.name }}</div>
    </template>
  </OVirtualList>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OVirtualList } from '@opensig/opendesign'

// 生成大量数据
const bigList = Array.from({ length: 10000 }, (_, i) => ({
  id: i,
  name: `列表项 ${i + 1}`,
}))

const dynamicList = Array.from({ length: 1000 }, (_, i) => ({
  title: `标题 ${i + 1}`,
  description: `这是第 ${i + 1} 项的描述内容，长度不固定`,
}))

const virtualListRef = ref()

const scrollToItem = (index: number) => {
  virtualListRef.value?.scrollToView(index, 'start', 'smooth')
}
</script>

<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: var(--o-gap-3) var(--o-gap-4);
  border-bottom: 1px solid var(--o-color-control1);
  height: 60px;
  box-sizing: border-box;
}

.card {
  padding: var(--o-gap-4);
  border-bottom: 1px solid var(--o-color-control1);
}
</style>
```

## 注意事项

- **必须设置容器高度**：父容器或组件本身需要有确定的高度（`height` 或 `max-height`），否则虚拟列表无法计算可视区域
- **固定高度优先**：已知列表项高度时务必传入 `itemSize`，性能远优于动态计算
- **列表项 key**：`#default` 插槽中如需使用 `v-for`，`:key` 应绑定到 `item` 的唯一标识，而非 `index`

## 导入方式

```vue
<script setup>
import { OVirtualList } from '@opensig/opendesign';
</script>
```
