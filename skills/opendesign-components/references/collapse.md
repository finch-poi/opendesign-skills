# OCollapse

折叠面板，用于对内容区域进行折叠/展开操作。

## 属性

**OCollapse：**

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `modelValue` | `string \| string[]` | — | 当前展开的面板 name（v-model），非 accordion 模式下为数组 |
| `accordion` | `boolean` | `false` | 手风琴模式，同时只能展开一项 |

**OCollapseItem：**

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `name` | `string` | — | 唯一标识，与 modelValue 对应 |
| `title` | `string` | — | 面板标题 |
| `disabled` | `boolean` | `false` | 禁用该面板 |

## 插槽

**OCollapseItem：**

| 插槽 | 说明 |
|------|------|
| `default` | 折叠面板的内容 |
| `title` | 自定义标题内容（优先级高于 `title` 属性） |

## 示例代码

```vue
<template>
  <!-- 基础用法 -->
  <OCollapse v-model="activeKey">
    <OCollapseItem title="标题1" name="1">
      内容1：折叠面板展示的内容区域
    </OCollapseItem>
    <OCollapseItem title="标题2" name="2">
      内容2：折叠面板展示的内容区域
    </OCollapseItem>
    <OCollapseItem title="标题3" name="3" disabled>
      内容3：禁用状态，无法折叠/展开
    </OCollapseItem>
  </OCollapse>

  <!-- 手风琴模式（同时只展开一项） -->
  <OCollapse accordion v-model="activeAccordion">
    <OCollapseItem title="第一项" name="a">内容A</OCollapseItem>
    <OCollapseItem title="第二项" name="b">内容B</OCollapseItem>
    <OCollapseItem title="第三项" name="c">内容C</OCollapseItem>
  </OCollapse>

  <!-- 自定义标题 -->
  <OCollapse v-model="activeKey">
    <OCollapseItem name="custom">
      <template #title>
        <span style="color: var(--o-color-primary1);">自定义标题</span>
      </template>
      自定义标题的内容
    </OCollapseItem>
  </OCollapse>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OCollapse, OCollapseItem } from '@opensig/opendesign'

// 非手风琴模式：支持多个展开，使用数组
const activeKey = ref<string[]>(['1'])

// 手风琴模式：只有一个展开，使用字符串
const activeAccordion = ref('a')
</script>
```

## 导入方式

```vue
<script setup>
import { OCollapse, OCollapseItem } from '@opensig/opendesign';
</script>
```
