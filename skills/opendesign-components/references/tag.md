# OTag

标签，用于标记和分类。

## 属性

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `color` | `'normal' \| 'primary' \| 'success' \| 'warning' \| 'danger'` | `'normal'` | 主题色 |
| `variant` | `'solid' \| 'outline'` | `'solid'` | 形状 |
| `size` | `'large' \| 'medium' \| 'small'` | `'large'` | 尺寸 |
| `round` | `string` | — | 圆角值（如 `'pill'`、`'4px'`） |
| `closable` | `boolean` | `false` | 是否可关闭（显示关闭按钮） |
| `visible` | `boolean` | `true` | 是否显示（v-model:visible） |
| `beforeClose` | `() => boolean \| Promise<boolean>` | — | 关闭前的钩子，返回 false 阻止关闭 |

## 插槽

| 插槽 | 说明 |
|------|------|
| `default` | 标签文本内容 |
| `icon` | 前缀图标 |

## 事件

| 事件 | 说明 |
|------|------|
| `close` | 点击关闭按钮时触发 |
| `update:visible` | 标签显示状态变化时触发 |

## 示例代码

```vue
<template>
  <!-- 基础用法 -->
  <OTag>默认标签</OTag>
  <OTag color="primary">主色标签</OTag>
  <OTag color="success">成功标签</OTag>
  <OTag color="warning">警告标签</OTag>
  <OTag color="danger">危险标签</OTag>

  <!-- 描边样式 -->
  <OTag color="primary" variant="outline">描边标签</OTag>

  <!-- 可关闭标签 -->
  <OTag color="primary" closable @close="handleClose">
    可关闭标签
  </OTag>

  <!-- 受控显示/隐藏 -->
  <OTag v-model:visible="tagVisible" closable>
    受控标签
  </OTag>

  <!-- 带图标 -->
  <OTag color="success">
    <template #icon>
      <OIconCheckCircle />
    </template>
    成功
  </OTag>

  <!-- 关闭前确认 -->
  <OTag closable :before-close="confirmClose">
    需确认关闭
  </OTag>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTag } from '@opensig/opendesign'

const tagVisible = ref(true)

const handleClose = () => {
  console.log('标签已关闭')
}

const confirmClose = () => {
  return window.confirm('确定要关闭吗？')
}
</script>
```

## 导入方式

```vue
<script setup>
import { OTag } from '@opensig/opendesign';
</script>
```
