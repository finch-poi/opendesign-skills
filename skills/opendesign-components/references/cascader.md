# OCascader

选中值: 通过 `modelValue` 完成双向绑定。`modelValue`的数据类型为`CascaderValueT`

圆角：通过 `round` 属性设置圆角，值为 `border-radius` 的值，或者 `pill`(半圆) 这个特殊值

按钮样式：通过 `variant` 属性设置按钮样式，值为 `solid`(实心)、`outline`(描边)、`text`(文字) 三种

选项框显示位置：通过 `optionPosition` 属性设置：

- `top`：顶部， `bottom`：底部，`left`：左侧，`right`：右侧
- `tl`, `tr`, `bl`, `br`, `lt`, `lb`, `rt`, `rb`：第一个字母表示位置，第二个字母表示对齐方式

  | 值  | 描述                 |
  | --- | -------------------- |
  | tl  | 显示在顶部，左对齐   |
  | tr  | 显示在顶部，右对齐   |
  | bl  | 显示在底部，左对齐   |
  | br  | 显示在底部，右对齐   |
  | lt  | 显示在左侧，顶部对齐 |
  | lb  | 显示在左侧，底部对齐 |
  | rt  | 显示在右侧，顶部对齐 |
  | rb  | 显示在右侧，底部对齐 |

选项: 通过 `options` 属性设置选项。`options` 的数据类型为 `CascaderOptionT[]`：

```ts:line-numbers
type CascaderNodeValueT = string | number;
type CascaderNodePathT = Array<CascaderNodeValueT>;
// modelValue 的数据类型
type CascaderValueT = CascaderNodeValueT | CascaderNodePathT;

// options 的数据类型
type CascaderOptionT = {
  value: CascaderNodeValueT;
  label?: string;
  children?: CascaderOptionT[];
};
```

## 示例代码

```vue
<OCascader
  v-model="ctx.modelValue"
  :options="ctx.options"
  
  class="cascader-doc-usage"
/>
<p>Selected: </p>
<pre>{{ ctx.modelValue }}</pre>
```

## 导入方式

```vue
<script setup>
import { OCascader } from '@opensig/opendesign';
</script>
```

