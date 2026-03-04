# OScrollbar

两种尺寸：`medium`、`small` ；

四种显示方式：`auto`、`always`、`hover`、`never` ；

滚动条显示方式为 `auto` 时,可以通过 `duration` 属性控制滚动条在停止滚动后持续显示的时间；

## 示例代码

```vue
<OScroller class="demo-scrollbar-usage-wrapper" >
        <div class="section">1</div>
        <div class="section">2</div>
        <div class="section">3</div>
      </OScroller>
```

## 导入方式

```vue
<script setup>
import { OScrollbar } from '@opensig/opendesign';
</script>
```

