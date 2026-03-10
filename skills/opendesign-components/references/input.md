# OInput

## 属性概览

**主题色 `color`**：`normal`（默认）、`success`、`warning`、`danger`

**尺寸 `size`**：`small`、`medium`（默认）、`large`

**形状 `variant`**：`solid`、`outline`（默认）、`text`

**圆角 `round`**：
- `round="pill"` — 半圆角
- `round="16px"` — 具体圆角值（带单位）
- 支持 `border-radius` 的任意合法值

## Props

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `modelValue` | `string` | — | 绑定值（v-model） |
| `color` | `'normal' \| 'success' \| 'warning' \| 'danger'` | `'normal'` | 主题色 |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | 尺寸 |
| `variant` | `'solid' \| 'outline' \| 'text'` | `'outline'` | 形状 |
| `round` | `string` | — | 圆角值 |
| `disabled` | `boolean` | `false` | 禁用 |
| `readonly` | `boolean` | `false` | 只读 |
| `clearable` | `boolean` | `false` | 可清空 |
| `maxLength` | `number` | — | 最大字符长度 |
| `showLength` | `boolean` | `false` | 显示输入字数/最大限制 |
| `inputOnOutlimit` | `boolean` | `false` | 超出最大字符数时是否允许继续输入 |
| `placeholder` | `string` | — | 占位文本 |
| `autoWidth` | `boolean` | `false` | 宽度随内容自适应 |
| `type` | `string` | `'text'` | input 原生 type（如 `'password'`） |

## 插槽

| 插槽 | 说明 |
|------|------|
| `prepend` | 输入框前置内容（外部，含边框） |
| `append` | 输入框后置内容（外部，含边框） |
| `prefix` | 输入框前缀图标（内部） |
| `suffix` | 输入框后缀图标（内部） |
| `extra` | 额外内容 |

## 事件

| 事件 | 类型 | 说明 |
|------|------|------|
| `update:modelValue` | `(value: string) => void` | 值变化时触发 |
| `change` | `(value: string) => void` | 值改变且失焦时触发 |
| `input` | `(value: string) => void` | 实时输入时触发 |
| `blur` | `(e: FocusEvent) => void` | 失焦时触发 |
| `focus` | `(e: FocusEvent) => void` | 聚焦时触发 |
| `clear` | `() => void` | 点击清空按钮时触发 |
| `pressEnter` | `(e: KeyboardEvent) => void` | 按下回车时触发 |

## 暴露方法

| 方法 | 说明 |
|------|------|
| `focus()` | 聚焦输入框 |
| `blur()` | 移除焦点 |
| `clear()` | 清空内容 |
| `inputEl()` | 获取原生 input 元素 |
| `togglePassword()` | 切换密码显示状态 |

## 示例代码

```vue
<template>
  <!-- 基础用法 -->
  <OInput v-model="inputVal" placeholder="请输入" />

  <!-- 带清空和字数统计 -->
  <OInput v-model="inputVal" clearable show-length :max-length="100" />

  <!-- 带前后缀 -->
  <OInput v-model="search" placeholder="搜索">
    <template #prefix>
      <OIconSearch />
    </template>
  </OInput>

  <!-- 带前置/后置内容 -->
  <OInput v-model="url" placeholder="请输入域名">
    <template #prepend>https://</template>
    <template #append>.com</template>
  </OInput>

  <!-- 校验状态 -->
  <OInput v-model="val" color="danger" placeholder="输入有误" />

  <!-- 密码框 -->
  <OInput v-model="password" type="password" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OInput } from '@opensig/opendesign'

const inputVal = ref('')
const search = ref('')
const url = ref('')
const val = ref('')
const password = ref('')
</script>
```

## 导入方式

```vue
<script setup>
import { OInput } from '@opensig/opendesign';
</script>
```
