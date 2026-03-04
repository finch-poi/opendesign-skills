# OCheckbox

多选框传值：

1. `value` 用于设置选中后 `modelValue` 的中包含的值
2. `modelValue` 的类型是 `Array<string | number>`，当选中后数组中会添加 `value`，否则会移除 `value`

半选：当 `indeterminate` 为 true 时，多选框将处于半选状态（无论 `modelValue` 是何值）。

多选框组：由于 `modelValue` 是一个数组，因此多选框组可以单独使用 `OCheckbox` 组件，也可以嵌套在 `OCheckboxGroup` 组件中。

## 示例代码

```vue
<OCheckbox
  v-model="ctx.modelValue"
  
  class="checkbox-doc-usage"
>
  Apple
</OCheckbox>
<p>Selected: {{ ctx.modelValue }}</p>
```

## 导入方式

```vue
<script setup>
import { OCheckbox } from '@opensig/opendesign';
</script>
```

