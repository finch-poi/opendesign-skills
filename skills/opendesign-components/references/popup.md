# OPopup

`OPopup` 是一个通用组件，像很多组件比如 `OPopover`、`ODropdown`、`OSelect` 都会用到该组件。该组件常用的属性如下：

1. 弹出窗通过 `visible` 属性进行双向绑定；
2. 弹出窗的位置可通过 `position` 属性控制；
3. 弹出窗的触发方式可通过 `trigger` 属性控制；
4. 弹出窗距离触发对象的距离可通过 `offset` 属性控制；
5. 弹出窗的锚点可通过 `anchor` 属性控制；
6. 弹出窗的宽度和最小宽度默认为触发对象的宽度，可以通过 `adjustMinWidth` 、 `adjustWidth` 属性调整；
7. 弹出窗的挂载容器的类名可以通过 `wrapClass` 添加，以此避免全局的样式污染；
8. 弹出窗的内容体的类名可以通过 `bodyClass` 添加，以此避免全局的样式污染；
9. 其他属性的说明请查看下方的 props 表。

## 示例代码

```vue
<div class="demo-popup-usage-wrap">
            <OPopup class="demo-popup-usage" wrapper=".demo-popup-usage-wrap" anchor-class="o-popover-anchor"  >
              <div>内容文本内容文本内容文本内容文本内容文本</div>
              <template #target>
                <OButton :disabled=${props.disabled} round="pill"> demo-popup </OButton>
              </template>
            </OPopup>
          </div>
```

## 导入方式

```vue
<script setup>
import { OPopup } from '@opensig/opendesign';
</script>
```

