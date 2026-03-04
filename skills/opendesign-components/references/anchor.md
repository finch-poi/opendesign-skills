# OAnchor

## `size` 属性
- 说明：指定锚点的尺寸风格（默认值：medium）

## `container` 属性
- 说明：指定锚点监听的滚动容器（默认值：window）
- 用法：组件会在该容器上监听 `scroll` 事件，以判断当前激活的锚点
- 示例：`container="#wrap"` 表示监听 id 为 wrap 的容器滚动事件

## `targetOffset` 属性
- 说明：目标元素跳转或激活时距离容器顶部的偏移量（默认值：0）
- 示例：`:target-offset="10"` 表示点击锚点时目标元素会滚动到距离容器顶部 10px 的位置；滚动距离小于 10px 时锚点处于激活状态

## `bounds` 属性
- 说明：设置锚点激活的判定边界（默认值：5）
- 用法：当需要跳转位置和激活判定边界不一致时可设置
- 示例：`:bounds="100" :target-offset="10"` 表示目标元素滚动到距离容器顶部 110px 时锚点激活。可实现点击锚点时目标元素滚动到顶部，滚动浏览时需到容器中上部才激活锚点的交互效果

## `changeHash` 属性
- 说明：是否在点击锚点时改变浏览器地址栏的 hash 值（默认值：true）
- 用法：如果需要手动控制 URL 跳转，可以设置为 false，并在 `click` 事件中处理跳转逻辑
- 示例：`:change-hash="false"` 表示点击锚点时不会改变浏览器地址栏的 hash 值

锚点嵌套：`OAnchorItem` 可以嵌套使用，形成多级锚点结构

## 示例代码

```vue
<div class="row demo-anchor-usage-wrap">
    <div id="wrap" class="demo-wrap">
      <div id="container-block1" class="block">container-block1</div>
      <div id="container-block1-1" class="block">container-block1-1</div>
      <div id="container-block2" class="block">container-block2</div>
      <div id="container-block2-1" class="block">container-block2-1</div>
      <div id="container-block2-2" class="block">container-block2-2</div>
      <div id="container-block2-2-1" class="block">container-block2-2-1</div>
      <div id="container-block4" class="block">container-block4</div>
      <div id="container-block5" class="block">container-block5</div>
      <div id="container-block5-1" class="block">container-block5-1</div>
    </div>
    <div class="demo-anchor">
      <OAnchor >
        <OAnchorItem href="#container-block1" title="container-block1">
          <OAnchorItem href="#container-block1-1" title="container-block1-1" />
        </OAnchorItem>
        <OAnchorItem href="#container-block2" title="container-block2">
          <OAnchorItem href="https://docs.openeuler.org" observe-href="#container-block2-1" title="自定义监听container-block2-1" />
          <OAnchorItem href="#container-block2-2" title="container-block2-2">
            <OAnchorItem href="#container-block2-2-1" title="container-block2-2-1换行openEuler Developer Day 2023 （简称 ODD 2023）是开放原子开源基金会旗下 openEuler 社区" />
          </OAnchorItem>
        </OAnchorItem>
        <OAnchorItem href="#container-block4" title="container-block4" />
        <OAnchorItem href="#container-block5" title="container-block5">
          <OAnchorItem href="#container-block5-1" title="container-block5-1" />
        </OAnchorItem>
      </OAnchor>
    </div>
  </div>
```

## 导入方式

```vue
<script setup>
import { OAnchor } from '@opensig/opendesign';
</script>
```

