# OMessage

消息提示组件，用于操作反馈信息的展示。支持内联使用和命令式调用两种方式。

## 内联使用

直接在模板中使用 `<OMessage>` 组件：

**Props：**

| 属性 | 类型 | 默认 | 说明 |
|------|------|------|------|
| `type` | `'info' \| 'success' \| 'warning' \| 'danger'` | `'info'` | 消息类型 |
| `closable` | `boolean` | `false` | 是否显示关闭按钮 |
| `icon` | `Component` | — | 自定义图标 |

```vue
<template>
  <OMessage type="info">这是一条提示信息</OMessage>
  <OMessage type="success">操作成功！</OMessage>
  <OMessage type="warning">请注意此操作的影响</OMessage>
  <OMessage type="danger">操作失败，请重试</OMessage>

  <!-- 可关闭 -->
  <OMessage type="success" closable>操作成功，点击关闭</OMessage>
</template>

<script setup lang="ts">
import { OMessage } from '@opensig/opendesign'
</script>
```

## 命令式调用

通过 `useMessage()` 或全局 `$message` 弹出浮动消息（自动消失）：

```vue
<template>
  <OButton @click="showMessage">显示消息</OButton>
</template>

<script setup lang="ts">
import { useMessage } from '@opensig/opendesign'

const message = useMessage()

const showMessage = () => {
  // 基础用法
  message.info('这是提示信息')
  message.success('操作成功！')
  message.warning('警告：操作有风险')
  message.danger('操作失败')

  // 带配置项
  message.success({
    content: '保存成功',
    duration: 3000,       // 自动关闭延时（ms），默认 3000
    closable: true,       // 显示关闭按钮
  })
}
</script>
```

## 使用场景

| 场景 | 方式 | 说明 |
|------|------|------|
| 表单校验提示、固定区域提示 | 内联 `<OMessage>` | 始终显示，不会自动消失 |
| 操作成功/失败反馈、API 响应提示 | 命令式 `useMessage()` | 浮动显示，自动消失 |

## 导入方式

```vue
<script setup>
import { OMessage, useMessage } from '@opensig/opendesign';
</script>
```
