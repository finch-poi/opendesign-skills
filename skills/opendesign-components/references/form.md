# OForm

目前`OForm` 支持的表单项有 `OInput`、`OInputNumber`、`OTextarea`、`OSelect`、`OCheckboxGroup`、`ORadioGroup`、`OUpload`

`layout`

- `h`: 水平布局（标签与控件在同一行）
- `v`: 垂直布局
- `inline`: 行内布局

`labelAlign`: 标签与控件之前垂直对其方式

- `top`: 标签顶部对其
- `center`: 标签居中对其
- `bottom`: 标签底部对其

`labelJustify`: 标签水平对齐方式

- `left`: 标签左对齐
- `center`: 标签居中对齐
- `right`: 标签右对齐

`labelWidth`: 标签宽度

`labelAlign` `labelJustify` 和 `labelWidth` 可通过 `OForm` 统一设置，也可通过 `OFormItem` 单独设置。

## 示例代码

```vue
<div>
  <OForm has-required >
    <OFormItem label="Title 1" required>
      <OInput />
    </OFormItem>
    <OFormItem label="Long title long title">
      <OSelect>
        <OOption v-for="item in ctx.options" :key="item.value" :label="item.label" :value="item.value" />
      </OSelect>
    </OFormItem>
    <OFormItem label="Title 3">
      <OTextarea />
    </OFormItem>
  </OForm>
</div>
```

## 导入方式

```vue
<script setup>
import { OForm } from '@opensig/opendesign';
</script>
```

