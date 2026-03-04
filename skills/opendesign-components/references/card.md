# OCard

OCard 分为图文卡片，和图标卡片。

1. 图文卡片：给 `cover` 设置图片链接，并可通过 `coverRadio` 设置该图片长宽比，通过 `coverFit` 设置图片填充方式
2. 图标卡片：给 `icon` 设置值，可以是图片链接或组件

通过 `layout` 设置卡片布局方式，包含垂直布局、水平布局以及水平反向布局

设置卡片标题

1. 通过 `title` 设置标题内容
2. 通过 `titleRow` 设置标题高度：`height: calc(title-row * line-height)`
3. 通过 `titleMaxRow` 设置标题最大行数，高于该行数时显示省略号。**注**：通过`-webkit-line-clamp`实现；一般而言 `titleRow` 的值与 `titleMaxRow` 值应该一致
4. 通过 `titleIcon` 设置标题开头的图标

设置卡片内容

1. 通过 `detail` 设置卡片内容
2. 通过 `detailRow` 设置内容高度 `height: calc(detail-row * line-height)`
3. 通过 `detailMaxRow` 设置内容最大行数，高于该行数时默认显示渐隐，可以通过设置 `textOverflow` 为 `ellipsis` 来显示省略号。**注**：通过`-webkit-line-clamp`实现；一般而言 `detailRow` 的值与 `detailMaxRow` 值应该一致

其它

1. `hoverable` 控制卡片是否有鼠标悬停阴影
2. `href` 设置卡片跳转链接；**注**：设置 `href` 属性后，卡片将以 `a` 标签渲染
3. `cursor` 控制鼠标悬停样式；当值为 `auto` 时，若设置了 `href` 属性，鼠标悬停样式为 `pointer`
4. `noResponsive` 值为真时，卡片尺寸 (间距、字体、行高等) 将不会随着视口尺寸改变而改变

## 导入方式

```vue
<script setup>
import { OCard } from '@opensig/opendesign';
</script>
```

