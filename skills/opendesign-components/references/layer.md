# OLayer

`transitionOrign`：设置内容盒子缩放动画的原点，即设置 css 属性 `transform-origin` 的值。取值有：

- `'mouse'`: 鼠标点击的位置（默认值）
- `'css'`: 通过 css 变量 `--layer-origin` 设置（`--layer-origin` 默认值为 `center`）

`wrapper`：设置浮层渲染的父节点。取值有：

- `'body'`: 渲染到 body 元素下（默认值），浮层的 `position` 属性为 `fixed`
- `string-selector`: 渲染到指定元素下，通过 `querySelector` 查询
- `HTMLElement`: 渲染到指定元素下
- `null`: 渲染到当前元素下，浮层的 `position` 属性为 `absolute`。
  **注**：若浮层元素的[包含块](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_display/Containing_block)是 `body` 元素，
  则浮层仍然会全屏覆盖，通常将当前元素的`position` 属性设置为 `relative` 来避免此情况。

`mask`：设置是否渲染遮罩层

`maskClose`：点击遮罩层时是否关闭浮层

`buttonClose`：是否渲染关闭按钮

## 导入方式

```vue
<script setup>
import { OLayer } from '@opensig/opendesign';
</script>
```

