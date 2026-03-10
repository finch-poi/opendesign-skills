# ORate

评分组件，支持只读、半星、可清除和自定义图标。

## Props

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `modelValue` | `number` | — | 绑定值（v-model），0 ~ count |
| `defaultValue` | `number` | `0` | 非受控模式下的默认值 |
| `count` | `number` | `5` | 星星总数 |
| `size` | `'large' \| 'medium'` | — | 尺寸 |
| `color` | `string` | `'normal'` | 主题色 |
| `readonly` | `boolean` | `false` | 只读模式 |
| `allowHalf` | `boolean` | `false` | 是否允许半星 |
| `clearable` | `boolean` | `false` | 再次点击同一值时是否清除 |
| `labels` | `string[]` | — | 各星级对应的描述文本（长度应等于 count） |
| `disabled` | `boolean` | `false` | 禁用 |

## 插槽

| 插槽 | 参数 | 说明 |
|------|------|------|
| `icon` | `{ index: number, status: 'active' \| 'half' \| 'inactive' }` | 自定义星标图标 |

## 事件

| 事件 | 类型 | 说明 |
|------|------|------|
| `update:modelValue` | `(val: number) => void` | 值变化时触发 |
| `change` | `(val: number) => void` | 点击确认后触发 |

## 示例代码

```vue
<template>
  <!-- 基础用法 -->
  <ORate v-model="score" />

  <!-- 允许半星 -->
  <ORate v-model="score" allow-half />

  <!-- 可清除 -->
  <ORate v-model="score" clearable />

  <!-- 只读 -->
  <ORate :model-value="3.5" allow-half readonly />

  <!-- 带描述文本 -->
  <ORate v-model="score" :labels="['很差', '较差', '一般', '较好', '很好']" />

  <!-- 自定义图标 -->
  <ORate v-model="score">
    <template #icon="{ status }">
      <OIconHeart :style="{ color: status === 'inactive' ? 'var(--o-color-control1)' : 'var(--o-color-danger1)' }" />
    </template>
  </ORate>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ORate } from '@opensig/opendesign'

const score = ref(3)
</script>
```

## 导入方式

```vue
<script setup>
import { ORate } from '@opensig/opendesign';
</script>
```
