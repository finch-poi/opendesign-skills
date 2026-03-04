# ODialog

### 尺寸

ODialog 提供了多种预设尺寸选项：`'exlarge'`、`'large'`、`'medium'`、`'small'` 和 `'auto'`，通过 `size` 属性进行设置。

不同尺寸的特点：

自适应尺寸 (`auto`)：

- 对话框会根据内容自动调整大小
- 适合内容长度不确定的场景

固定尺寸 (exlarge/large/medium/small)：

- 对话框具有固定宽度
- 高度会根据内容自动调整，但不会超过预设的最大及最小高度

视宽适配：

- 默认情况下，对话框会根据视口大小自动调整尺寸（如间距，宽度，高度范围，字号等）
- 如需禁用自动适配，可设置 `noResponsive` 为 `true`
- 也可通过 CSS 变量进行精细的尺寸定制

移动端半屏显示：

- 设置 `phoneHalfFull` 为 `true` 时，在小屏幕设备（宽度 < 600px）上对话框宽度占满整个视口，显示在底部
- 注意：此时 size 属性仅影响高度，宽度固定为全屏；不能同时设置 noResponsive 为 true

## 导入方式

```vue
<script setup>
import { ODialog } from '@opensig/opendesign';
</script>
```

