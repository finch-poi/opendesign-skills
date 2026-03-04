# OCarousel

幻灯片有两种播放效果滚动和切换

- 将 `effect` 设置为 `gallery` (默认值) 为滚动效果。当为滚动效果时，可以将 `OCarouselItem` 的宽度设置为略小于 `OCarousel` 的宽度，
  这样可以将当前激活的幻灯片两侧的幻灯片显示出来，此时 `clickToSwitch` 参数才会有效果。

  ![示意图](./half.zh-CN.png)
- 将 `effect` 设置为 `toggle` 为切换效果

自动播放

- 将 `autoPlay` 设置为 `true` 开启自动播放
- `interval` 设置自动播放间隔时间, 默认值为 5000ms
- `pauseOnHover` 鼠标悬停时暂停播放

指示器切换

- `hideIndicator` 隐藏指示器
- `indicatorClick` 允许点击指示器切换幻灯片

箭头切换

- `arrow` 设置箭头显示方式，默认值为 `hover`
- 点击箭头可切换幻灯片

卡片点击切换： `clickToSwitch` 允许点击卡片切换幻灯片

其它：

- `manualInit` 允许手动初始化；手动初始化需要调用 `instance.init()` 完成初始化
- `activeIndex` 当前激活的幻灯片索引，可双向绑定
- `arrowWrapClass` 箭头容器类名，方便自定义箭头样式
- `indicatorWrapClass` 指示器容器类名，方便自定义指示器样式

## 导入方式

```vue
<script setup>
import { OCarousel } from '@opensig/opendesign';
</script>
```

