# ORadio

单选框传值：

1. `value` 用于设置选中后 `modelValue` 的值
2. `modelValue` 的类型是 `string | number | boolean`，当选中后 `modelValue` 的值为 `value` 值

单选框组：当单选框的数量较多时，单选框组可以用来简化 `v-model` 的书写，此时将 `v-model` 写在单选框组上即可

## 示例代码

```vue
<div class="demo-radio-usage-wrap">
  <ORadio class="demo-radio-usage" v-model="ctx.radioVal"  >Apple</ORadio>
    <div class="demo-radio-val">
    Selected：{{ ctx.radioVal }}
  </div></div>
```

## 导入方式

```vue
<script setup>
import { ORadio } from '@opensig/opendesign';
</script>
```

