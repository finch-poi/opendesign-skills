# OButton

按钮包含 `normal`（默认）、`brand` 两种主题色；

三种尺寸：`small`、`medium`、`large` ；

三种形状：`solid`、`outline`、`text` ；

禁用状态：`disabled` ；

加载状态：`loading` ；

按钮的圆角可以通过 `round` 属性设置：
- `round="pill"` 设置为半圆角
- `round="16px"` 设置为具体的圆角值（必须带单位，如 `px`）
- 可以是 css 属性 `border-radius` 能够接受的任意值（如 `"16px"`, `"1rem"`, `"50%"` 等）

## 导入方式

```vue
<script setup>
import { OButton } from '@opensig/opendesign';
</script>
```

