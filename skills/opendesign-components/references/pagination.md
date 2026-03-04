# OPagination

`layout`: 设置显示的控件，通过数组组合

- `total`: 总数据量标签
- `pagesize`: 每页数据条数选择器
- `pager`: 页码按钮
- `jumper`: 页码跳转输入框

`variant`: 按钮形状

- `outline`: 空心按钮
- `solid`: 实心按钮

`showPageCount`: 最多显示多少个页码按钮

`showMore`: 当鼠标悬停省略按钮时是否弹出省略的页码（当总页数多余 `showPageCount` 时显示省略按钮）

`simple`: 是否使用简单布局。使用简单布局时，`layout` 以及 `showPageCount` 属性失效

## 导入方式

```vue
<script setup>
import { OPagination } from '@opensig/opendesign';
</script>
```

