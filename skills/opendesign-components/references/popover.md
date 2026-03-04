# OPopover

`OPopover` 组件本质上与 `OPopup` 没有太大区别，主要的一些差异点是 `OPopover` 调整了 `trigger`、`offset`、`anchor` 属性的默认值，并在 `OPopup` 外部控制`disable`的两种状态。

1. 弹出窗的位置可通过 `position` 属性控制；
2. 弹出窗的触发方式可通过 `trigger` 属性控制；
3. 弹出窗距离触发对象的距离可通过 `offset` 属性控制；
4. 弹出窗的宽度和最小宽度默认为触发对象的宽度，可以通过 `adjustMinWidth` 、 `adjustWidth` 属性调整；
5. 弹出窗的挂载容器的类名可以通过 `wrapClass` 添加，以此避免全局的样式污染；
6. 其他属性的说明请查看下方的 props 表。

## 示例代码

```vue
<div class="demo-popover-usage-wrap">
            <OPopover class="demo-popover-usage" >
              <div>内容文本内容文本内容文本内容文本内容文本</div>
              <template #target>
                <OButton :disabled=${props.disabled} round="pill"> demo-popover </OButton>
              </template>
            </OPopover>
          </div>
```

## 导入方式

```vue
<script setup>
import { OPopover } from '@opensig/opendesign';
</script>
```

