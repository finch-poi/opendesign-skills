# OInput

输入框包含 `primary`、`success`、`warning`、`danger` 四种主题色；

三种尺寸：`small`、`medium`、`large` ；

三种形状：`solid`、`outline`、`text` ；

禁用状态：`disabled` ；

通过属性 `showLength` 控制输入字符数与最大限制字符数的展示与隐藏；

通过属性 `maxLength` 限制输入最大字符长度；

通过属性 `inputOnOutlimit` 控制输入字符超长时，是否允许继续输入；

按钮的圆角可以通过 `pill` 设置为半圆，也可以是 css 属性 `border-radius` 能够接受的其它值。

## 示例代码

```vue
<OInput v-model="ctx.inputVal"   /> 
    <div class="doc-input-text-wrap"><span>输入的值：</span>{{ctx.inputVal}}</div>
```

## 导入方式

```vue
<script setup>
import { OInput } from '@opensig/opendesign';
</script>
```

