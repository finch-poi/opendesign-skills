# OGrid

ORow的属性：

通过属性 `inline` 控制 `Row` 的根元素的 `display` 是否为 `inline-flex`；

通过属性 `align` 控制容器辅轴对齐方式；

通过属性 `justify` 控制容器主轴对齐方式；

通过属性 `wrap` 控制容器 `flex-wrap` 样式的值；

通过属性 `direction` 控制容器 `flex-direction` 样式的值；

通过属性 `gap` 控制子元素的间距，注意：当同时为组件传递了 `gap`、`gapX`、`gapY` 属性，将优先使用 `gapX`、`gapY`；

通过属性 `pcS`、`laptop`、`pad`、`padV`、`phone` 可以控制不同断点尺寸下的 `gap`值。

OCol的属性：

通过属性 `flex` 控制元素的 `flex` 样式的值；

通过属性 `align` 控制元素辅轴的对齐方式；

通过属性 `pcS`、`laptop`、`pad`、`padV`、`phone` 可以控制不同断点尺寸下的 `flex`值。

## 导入方式

```vue
<script setup>
import { OGrid } from '@opensig/opendesign';
</script>
```

