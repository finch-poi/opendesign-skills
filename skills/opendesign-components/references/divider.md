# ODivider

### 使用说明

#### 参数配置

- **variant**：控制分割线形状
  可选值：`solid`（实线）、`dashed`（虚线）、`dotted`（点线）

- **direction**：控制分割线方向
  可选值：`h`（水平）、`v`（垂直）

  - 水平分割线（`direction="h"`）默认宽度占满容器；
  - 垂直分割线（`direction="v"`）默认高度为 `1em`。

- **darker**：控制分割线颜色深浅
  可选值：`true`（深色）、`false`（浅色）

#### 标签

- **限制**：仅水平分割线（`direction="h"`）支持标签功能。
- **标签位置**：通过 `labelPosition` 属性控制，可选值：`left`（左侧）、`center`（中间）、`right`（右侧）。
- **标签内容**：标签文本需放置在组件的 `default` 插槽中。

## 导入方式

```vue
<script setup>
import { ODivider } from '@opensig/opendesign';
</script>
```

