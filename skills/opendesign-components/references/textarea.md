# OTextarea

多行文本输入框。

## Props

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `modelValue` | `string` | — | 绑定值（v-model） |
| `color` | `'normal' \| 'success' \| 'warning' \| 'danger'` | `'normal'` | 主题色 |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | 尺寸 |
| `variant` | `'solid' \| 'outline' \| 'text'` | `'outline'` | 形状 |
| `disabled` | `boolean` | `false` | 禁用 |
| `readonly` | `boolean` | `false` | 只读 |
| `clearable` | `boolean` | `false` | 可清空 |
| `maxLength` | `number` | — | 最大字符数限制 |
| `showLength` | `boolean` | `false` | 显示字数统计 |
| `placeholder` | `string` | — | 占位文本 |
| `autoSize` | `boolean \| { minRows?: number; maxRows?: number }` | `false` | 自动调整高度（`true` 无限制，对象可指定最小/最大行数） |
| `resize` | `'none' \| 'vertical' \| 'horizontal' \| 'both'` | `'none'` | 是否允许手动调整大小 |
| `scrollbar` | `boolean` | `true` | 是否显示滚动条 |
| `rows` | `number` | — | 初始显示行数（原生 rows 属性） |

## 插槽

| 插槽 | 说明 |
|------|------|
| `prepend` | 前置内容（外部） |
| `append` | 后置内容（外部） |
| `suffix` | 后缀内容（内部右下角） |

## 事件

| 事件 | 类型 | 说明 |
|------|------|------|
| `update:modelValue` | `(value: string) => void` | 值变化时触发 |
| `change` | `(value: string) => void` | 值改变且失焦时触发 |
| `input` | `(value: string) => void` | 实时输入时触发 |
| `blur` | `(e: FocusEvent) => void` | 失焦时触发 |
| `focus` | `(e: FocusEvent) => void` | 聚焦时触发 |
| `clear` | `() => void` | 点击清空按钮时触发 |

## 暴露方法

| 方法 | 说明 |
|------|------|
| `focus()` | 聚焦 |
| `blur()` | 移除焦点 |
| `clear()` | 清空内容 |
| `inputEl()` | 获取原生 textarea 元素 |

## 示例代码

```vue
<template>
  <!-- 基础用法 -->
  <OTextarea v-model="content" placeholder="请输入内容" />

  <!-- 自动调整高度（3~8行） -->
  <OTextarea
    v-model="content"
    :auto-size="{ minRows: 3, maxRows: 8 }"
    placeholder="内容区域会随输入自动调整高度"
  />

  <!-- 字数统计 -->
  <OTextarea
    v-model="content"
    :max-length="500"
    show-length
    placeholder="最多输入500字"
  />

  <!-- 可清空 + 校验状态 -->
  <OTextarea v-model="content" clearable color="danger" placeholder="输入有误" />

  <!-- 固定高度 + 可手动拖拽 -->
  <OTextarea v-model="content" :rows="6" resize="vertical" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTextarea } from '@opensig/opendesign'

const content = ref('')
</script>
```

## 导入方式

```vue
<script setup>
import { OTextarea } from '@opensig/opendesign';
</script>
```
