# OSelect

选择框包含 `normal`（默认）、`success`、`warning`、`danger` 四种主题色；

三种尺寸：`small`、`medium`、`large` ；

三种形状：`solid`、`outline`、`text` ；

禁用状态：`disabled` ；

支持多选：`multiple` ；

选择框的圆角可以通过 `pill` 设置为半圆，也可以是 css 属性 `border-radius` 能够接受的其它值；

其他属性的说明请查看下方的 props 表。

## 示例代码

```vue
<div class="demo-select-usage-wrap">
  <OSelect v-model=ctx.selectedVal class="demo-select-usage" option-title="选项标题"   :max-tag-count="2">
   <OOption v-for="item in ctx.options" :key="item.value" :label="item.label" :value="item.value" />
  </OSelect>
   </div>
```

## 导入方式

```vue
<script setup>
import { OSelect } from '@opensig/opendesign';
</script>
```

