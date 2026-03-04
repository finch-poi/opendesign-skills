---
name: opendesign-components
description: OpenDesign 组件库使用指南。当需要使用 OpenDesign Vue 组件库快速搭建页面时使用此 skill。支持所有 OpenDesign 组件，包括按钮、表单、表格、对话框、卡片等常用 UI 组件。使用场景：(1) 使用 OpenDesign 组件构建 Vue 页面，(2) 查找组件使用方法和属性说明，(3) 获取组件代码示例
---

# OpenDesign 组件库使用指南

OpenDesign 是一个功能丰富的 Vue 3 组件库，提供了大量可复用的 UI 组件。

## 安装

### 1. 安装依赖包

OpenDesign 需要安装两个包：

```bash
pnpm add @opensig/opendesign @opensig/opendesign-token
# 或
npm install @opensig/opendesign @opensig/opendesign-token
```

**重要说明：**
- `@opensig/opendesign` - 组件库本身
- `@opensig/opendesign-token` - 设计 token（必需），包含主题变量和样式基础

### 2. 引入样式文件

**必须在项目入口文件（如 `main.ts`）中按顺序引入以下样式：**

```typescript
// main.ts
import '@opensig/opendesign-token/themes/e.token.css'  // 1. 先引入 token 变量
import '@opensig/opendesign/es/index.scss'              // 2. 再引入组件样式

import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

**注意事项：**
1. **引入顺序很重要**：必须先引入 token.css，再引入组件样式
2. **文件扩展名**：token 文件是 `.css`，组件样式是 `.scss`
3. **不要只引入** `@opensig/opendesign/dist/index.css`，这样会缺少 token 变量导致样式错误
4. 如果页面样式显示不正常，首先检查是否正确引入了这两个样式文件

### 3. 常见问题

**问题：页面样式混乱或组件显示不正常**

解决方案：
1. 检查是否安装了 `@opensig/opendesign-token` 包
2. 检查 `main.ts` 中是否按正确顺序引入了两个样式文件
3. 确认引入的是 `e.token.css`（不是 `.scss`）
4. 确认引入的是 `es/index.scss`（不是 `dist/index.css`）

## 快速开始

所有组件都从 `@opensig/opendesign` 导入：

```vue
<script setup>
import { OButton, OInput, OCard } from '@opensig/opendesign';
</script>
```

## 组件列表

以下是所有可用组件的快速参考。每个组件都有详细的使用说明和示例代码。

### 组件索引

- [OAnchor](#anchor) - Anchor
- [OBadge](#badge) - Badge
- [OBreadcrumb](#breadcrumb) - Breadcrumb
- [OButton](#button) - Button
- [OCard](#card) - Card
- [OCarousel](#carousel) - Carousel
- [OCascader](#cascader) - Cascader
- [OCheckbox](#checkbox) - Checkbox
- [OCollapse](#collapse) - Collapse
- [ODialog](#dialog) - Dialog
- [ODivider](#divider) - Divider
- [ODropdown](#dropdown) - Dropdown
- [OFigure](#figure) - Figure
- [OForm](#form) - Form
- [OGrid](#grid) - Grid
- [OInput](#input) - Input
- [OLayer](#layer) - Layer
- [OLink](#link) - Link
- [OLoading](#loading) - Loading
- [OMenu](#menu) - Menu
- [OMessage](#message) - Message
- [OPagination](#pagination) - Pagination
- [OPopover](#popover) - Popover
- [OPopup](#popup) - Popup
- [OProgress](#progress) - Progress
- [ORadio](#radio) - Radio
- [ORate](#rate) - Rate
- [OResult](#result) - Result
- [OScrollbar](#scrollbar) - Scrollbar
- [OSelect](#select) - Select
- [OSkeleton](#skeleton) - Skeleton
- [OSwitch](#switch) - Switch
- [OTab](#tab) - Tab
- [OTable](#table) - Table
- [OTag](#tag) - Tag
- [OTextarea](#textarea) - Textarea
- [OToggle](#toggle) - Toggle
- [OUpload](#upload) - Upload
- [OVirtualList](#virtual-list) - Virtual List

---

## OAnchor

**`size`** 属性
- 说明：指定锚点的尺寸风格（默认值：medium）

**`container`** 属性
- 说明：指定锚点监听的滚动容器（默认值：window）
- 用法：组件会在该容器上监听 `scroll` 事件，以判断当前激活的锚点
- 示例：`container="#wrap"` 表示监听 id 为 wrap 的容器滚动事件

**`targetOffset`** 属性
- 说明：目标元素跳转或激活时距离容器顶部的偏移量（默认值：0）
- 示例：`:target-offset="10"` 表示点击锚点时目标元素会滚动到距离容器顶部 10px 的位置；滚动距离小于 10px 时锚点处于激活状态

**`bounds`** 属性
- 说明：设置锚点激活的判定边界（默认值：5）
- 用法：当需要跳转位置和激活判定边界不一致时可设置
- 示例：`:bounds="100" :target-offset="10"` 表示目标元素滚动到距离容器顶部 110px 时锚点激活。可实现点击锚点时目标元素滚动到顶部，滚动浏览时需到容器中上部才激活锚点的交互效果

**`changeHash`** 属性
- 说明：是否在点击锚点时改变浏览器地址栏的 hash 值（默认值：true）
- 用法：如果需要手动控制 URL 跳转，可以设置为 false，并在 `click` 事件中处理跳转逻辑
- 示例：`:change-hash="false"` 表示点击锚点时不会改变浏览器地址栏的 hash 值

锚点嵌套：`OAnchorItem` 可以嵌套使用，形成多级锚点结构

### 示例代码

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

> 详细使用说明和完整属性列表，请查看 [references/anchor.md](references/anchor.md)


---

## OBadge

徽标包含 `primary`、`success`、`warning`、`danger` 四种主题色。

徽标 `value` 参数支持数字和文本两种类型的值，当为数字时 `max` 参数会影响值的显示。

徽标支持小红点样式，小红点中不会显示徽标内容。

徽标可以通过 `offset` 设置偏移位置。


---

## OBreadcrumb

### 基础用法

通过 `href` 属性设置链接跳转地址，或者使用 `to` 属性配合 Vue Router 实现路由跳转。当 `href` 和 `to` 属性都未设置时，`OBreadcrumbItem` 组件会使用 `span` 标签渲染为一个普通的文本（这对于 SEO 是有好处的）。

`href` 属性和 `target` 属性组合使用，`to` 属性和 `replace` 属性组合使用，当同时传递 `href` 属性和 `to` 属性时，会优先使用 `to` 形式的跳转。

### 示例代码

```vue
<OBreadcrumb>
    <OBreadcrumbItem  >Home</OBreadcrumbItem>
    <OBreadcrumbItem>Current Page</OBreadcrumbItem>
  </OBreadcrumb>
```

> 详细使用说明和完整属性列表，请查看 [references/breadcrumb.md](references/breadcrumb.md)


---

## OButton

按钮包含 `primary`、`success`、`warning`、`danger` `brand` 五种主题色；

三种尺寸：`small`、`medium`、`large` ；

三种形状：`solid`、`outline`、`text` ；

禁用状态：`disabled` ；

加载状态：`loading` ；

按钮的圆角可以通过 `round` 属性设置：
- `round="pill"` 设置为半圆角
- `round="16px"` 设置为具体的圆角值（必须带单位，如 `px`）
- 可以是 css 属性 `border-radius` 能够接受的任意值（如 `"16px"`, `"1rem"`, `"50%"` 等）


---

## OCard

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


---

## OCarousel

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


---

## OCascader

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

### 示例代码

```vue
<OCascader
  v-model="ctx.modelValue"
  :options="ctx.options"
  
  class="cascader-doc-usage"
/>
<p>Selected: </p>
<pre>{{ ctx.modelValue }}</pre>
```

> 详细使用说明和完整属性列表，请查看 [references/cascader.md](references/cascader.md)


---

## OCheckbox

多选框传值：

1. `value` 用于设置选中后 `modelValue` 的中包含的值
2. `modelValue` 的类型是 `Array<string | number>`，当选中后数组中会添加 `value`，否则会移除 `value`

半选：当 `indeterminate` 为 true 时，多选框将处于半选状态（无论 `modelValue` 是何值）。

多选框组：由于 `modelValue` 是一个数组，因此多选框组可以单独使用 `OCheckbox` 组件，也可以嵌套在 `OCheckboxGroup` 组件中。

### 示例代码

```vue
<OCheckbox
  v-model="ctx.modelValue"
  
  class="checkbox-doc-usage"
>
  Apple
</OCheckbox>
<p>Selected: {{ ctx.modelValue }}</p>
```

> 详细使用说明和完整属性列表，请查看 [references/checkbox.md](references/checkbox.md)


---

## OCollapse

通过 `accordion` 属性开启手风情模式；


---

## ODialog

### 尺寸

ODialog 提供了多种预设尺寸选项：`'exlarge'`、`'large'`、`'medium'`、`'small'` 和 `'auto'`，通过 `size` 属性进行设置。

不同尺寸的特点：

自适应尺寸 (`auto`)：

- 对话框会根据内容自动调整大小
- 适合内容长度不确定的场景

固定尺寸 (exlarge/large/medium/small)：

- 对话框具有固定宽度
- 高度会根据内容自动调整，但不会超过预设的最大及最小高度

视宽适配：

- 默认情况下，对话框会根据视口大小自动调整尺寸（如间距，宽度，高度范围，字号等）
- 如需禁用自动适配，可设置 `noResponsive` 为 `true`
- 也可通过 CSS 变量进行精细的尺寸定制

移动端半屏显示：

- 设置 `phoneHalfFull` 为 `true` 时，在小屏幕设备（宽度 < 600px）上对话框宽度占满整个视口，显示在底部
- 注意：此时 size 属性仅影响高度，宽度固定为全屏；不能同时设置 noResponsive 为 true


---

## ODivider

### 使用说明

#### 参数配置

- **variant**：控制分割线形状
  可选值：`solid`（实线）、`dashed`（虚线）、`dotted`（点线）

- **direction**：控制分割线方向
  可选值：`h`（水平）、`v`（垂直）

  - 水平分割线（`direction="h"`）默认宽度占满容器；
  - 垂直分割线（`direction="v"`）默认高度为 `1em`。

- **darker**：控制分割线颜色深浅
  可选值：`true`（深色）、`false`（浅色）

#### 标签

- **限制**：仅水平分割线（`direction="h"`）支持标签功能。
- **标签位置**：通过 `labelPosition` 属性控制，可选值：`left`（左侧）、`center`（中间）、`right`（右侧）。
- **标签内容**：标签文本需放置在组件的 `default` 插槽中。


---

## ODropdown

下拉选项触发方式：`none`、`click`、`click-outclick`、`hover`、`hover-outclick`、`focus`、`contextmenu`；

下拉选项位置：`top`、`tl`、`tr`、`bottom`、`bl`、`br`、`left`、`lt`、`lb`、`right`、`rt`、`rb`；

### 示例代码

```vue
<ODropdown  style="width:fit-content;">
  <OButton color="primary"  round="pill">Dropdown
    <template #suffix>
      <OIconChevronDown class="icon"  />
    </template></OButton>
  <template #dropdown>
  ${createTemplate(options)}
  </template>
  </ODropdown>
```

> 详细使用说明和完整属性列表，请查看 [references/dropdown.md](references/dropdown.md)


---

## OFigure

### 使用说明

#### 属性说明

**`ratio`**: 图片宽高比控制

- 通过 `padding-top` 百分比实现宽高比
- 子元素使用 `absolute` 定位填充容器。这会覆盖 `<img>` 元素的固有宽高比特性
- 基于以上两点必要时显式设置容器宽度，否则容器宽高可能坍塌为 0，导致图片无法显示

**`fit`**: 图片填充模式（默认：`contain`）

- `background=false` 时（使用 `<img>` 标签）：
  - 通过 [object-fit](https://developer.mozilla.org/zh-CN/docs/Web/CSS/object-fit) 控制
  - 可选值：`cover` | `contain` | `fill` | `none` | `scale-down`
- `background=true` 时（使用背景图）：
  - 通过 [background-size](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size) 控制
  - 可选值：`cover` | `contain` | `auto` | `<length>` | `<percentage>`
  - 示例：`fit="100% 80%"` 可设置自定义背景图尺寸
  - 注意：由于不再使用 `<img>` 标签渲染，可能导致宽高塌陷

**`hoverable`**: 悬停放大效果

- 自动生效场景（无需显式设置该属性）：
  - `href` 存在时（链接跳转）
  - `preview=true`（图片预览）
  - `videoPoster=true`（视频海报）
- 当需要**独立控制**悬停效果时使用

**`preview`**: 点击预览功能，启用后会接管点击事件（显示全屏预览层）

**`previewClose`**: 预览关闭方式

- 可选值：
  - `'none'`：禁用关闭
  - `'mask'`：点击遮罩层关闭
  - `'button'`：点击关闭按钮
  - `'body'`：点击预览图片关闭
- 组合模式：支持数组配置（如 `['mask','button']`）
- 默认值：
  - 📱 Pad 端（视口 < 1200px 的触屏设备）：`['mask','button']`
  - 💻 PC 端：`['mask','button','body']`

**`href`**: 链接跳转

- 启用后组件渲染为 `<a>` 标签
- 行为：点击执行页面跳转

#### 互斥属性冲突

`preview`, `href` **禁止同时启用**（两者均会接管点击事件）


---

## OForm

目前`OForm` 支持的表单项有 `OInput`、`OInputNumber`、`OTextarea`、`OSelect`、`OCheckboxGroup`、`ORadioGroup`、`OUpload`

`layout`

- `h`: 水平布局（标签与控件在同一行）
- `v`: 垂直布局
- `inline`: 行内布局

`labelAlign`: 标签与控件之前垂直对其方式

- `top`: 标签顶部对其
- `center`: 标签居中对其
- `bottom`: 标签底部对其

`labelJustify`: 标签水平对齐方式

- `left`: 标签左对齐
- `center`: 标签居中对齐
- `right`: 标签右对齐

`labelWidth`: 标签宽度

`labelAlign` `labelJustify` 和 `labelWidth` 可通过 `OForm` 统一设置，也可通过 `OFormItem` 单独设置。

### 示例代码

```vue
<div>
  <OForm has-required >
    <OFormItem label="Title 1" required>
      <OInput />
    </OFormItem>
    <OFormItem label="Long title long title">
      <OSelect>
        <OOption v-for="item in ctx.options" :key="item.value" :label="item.label" :value="item.value" />
      </OSelect>
    </OFormItem>
    <OFormItem label="Title 3">
      <OTextarea />
    </OFormItem>
  </OForm>
</div>
```

> 详细使用说明和完整属性列表，请查看 [references/form.md](references/form.md)


---

## OGrid

ORow的属性：

通过属性 `inline` 控制 `Row` 的根元素的 `display` 是否为 `inline-flex`；

通过属性 `align` 控制容器辅轴对齐方式；

通过属性 `justify` 控制容器主轴对齐方式；

通过属性 `wrap` 控制容器 `flex-wrap` 样式的值；

通过属性 `direction` 控制容器 `flex-direction` 样式的值；

通过属性 `gap` 控制子元素的间距，注意：当同时为组件传递了 `gap`、`gapX`、`gapY` 属性，将优先使用 `gapX`、`gapY`；

通过属性 `pcS`、`laptop`、`pad`、`padV`、`phone` 可以控制不同断点尺寸下的 `gap`值。

OCol的属性：

通过属性 `flex` 控制元素的 `flex` 样式的值；

通过属性 `align` 控制元素辅轴的对齐方式；

通过属性 `pcS`、`laptop`、`pad`、`padV`、`phone` 可以控制不同断点尺寸下的 `flex`值。


---

## OInput

输入框包含 `primary`、`success`、`warning`、`danger` 四种主题色；

三种尺寸：`small`、`medium`、`large` ；

三种形状：`solid`、`outline`、`text` ；

禁用状态：`disabled` ；

通过属性 `showLength` 控制输入字符数与最大限制字符数的展示与隐藏；

通过属性 `maxLength` 限制输入最大字符长度；

通过属性 `inputOnOutlimit` 控制输入字符超长时，是否允许继续输入；

按钮的圆角可以通过 `pill` 设置为半圆，也可以是 css 属性 `border-radius` 能够接受的其它值。

### 示例代码

```vue
<OInput v-model="ctx.inputVal"   /> 
    <div class="doc-input-text-wrap"><span>输入的值：</span>{{ctx.inputVal}}</div>
```

> 详细使用说明和完整属性列表，请查看 [references/input.md](references/input.md)


---

## OLayer

`transitionOrign`：设置内容盒子缩放动画的原点，即设置 css 属性 `transform-origin` 的值。取值有：

- `'mouse'`: 鼠标点击的位置（默认值）
- `'css'`: 通过 css 变量 `--layer-origin` 设置（`--layer-origin` 默认值为 `center`）

`wrapper`：设置浮层渲染的父节点。取值有：

- `'body'`: 渲染到 body 元素下（默认值），浮层的 `position` 属性为 `fixed`
- `string-selector`: 渲染到指定元素下，通过 `querySelector` 查询
- `HTMLElement`: 渲染到指定元素下
- `null`: 渲染到当前元素下，浮层的 `position` 属性为 `absolute`。
  **注**：若浮层元素的[包含块](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_display/Containing_block)是 `body` 元素，
  则浮层仍然会全屏覆盖，通常将当前元素的`position` 属性设置为 `relative` 来避免此情况。

`mask`：设置是否渲染遮罩层

`maskClose`：点击遮罩层时是否关闭浮层

`buttonClose`：是否渲染关闭按钮


---

## OLink

五种主题色：`normal`、`primary`、`success`、`warning`、`danger` ；

四种尺寸：`auto`、`small`、`medium`、`large` ；

四种跳转方式：`_blank`、`_parent`、`_self`、`_top` ；

禁用状态：`disabled` ；

加载状态：`loading` ；


---

## OLoading

通过 `label` 属性控制 loading 时显示的文本；

通过 `icon` 属性自定义 loading 时的图标；

通过 `iconRotating` 属性控制自定义的 loading 图标是否旋转；

其它属性的使用详见[OLayer](/zh-CN/components/layer#使用)。


---

## OMenu

两种尺寸：`small`、`medium` ；

通过 `accordion` 属性开启手风情模式；

通过 `expanded` 属性控制展开的节点值；

通过 `subMenu` 的 `icon` 控制菜单的图标。注意：`small` 尺寸的 `menu` 不支持自定义图标；

通过 `selectable` 可以控制 `subMenu` 本身是否可以被选中；

通过css变量 `--menu-item-base-indent`、`--sub-menu-base-indent` 控制层级缩进距离。


---

## OMessage

### 内联

### 示例代码

```vue
<OMessage >${props.content}</OMessage>
```

> 详细使用说明和完整属性列表，请查看 [references/message.md](references/message.md)


---

## OPagination

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


---

## OPopover

`OPopover` 组件本质上与 `OPopup` 没有太大区别，主要的一些差异点是 `OPopover` 调整了 `trigger`、`offset`、`anchor` 属性的默认值，并在 `OPopup` 外部控制`disable`的两种状态。

1. 弹出窗的位置可通过 `position` 属性控制；
2. 弹出窗的触发方式可通过 `trigger` 属性控制；
3. 弹出窗距离触发对象的距离可通过 `offset` 属性控制；
4. 弹出窗的宽度和最小宽度默认为触发对象的宽度，可以通过 `adjustMinWidth` 、 `adjustWidth` 属性调整；
5. 弹出窗的挂载容器的类名可以通过 `wrapClass` 添加，以此避免全局的样式污染；
6. 其他属性的说明请查看下方的 props 表。

### 示例代码

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

> 详细使用说明和完整属性列表，请查看 [references/popover.md](references/popover.md)


---

## OPopup

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

### 示例代码

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

> 详细使用说明和完整属性列表，请查看 [references/popup.md](references/popup.md)


---

## OProgress

两种类型：`line`、`circle`；

两种尺寸：`medium`、`small` ；

四种颜色：`primary`、`success`、`warning`、`danger`；

进度条百分比通过 `percentage` 属性控制；

进度条线宽通过 `strokeWidth` 属性控制；

进度条轨道宽度通过 `trackWidth` 属性控制；


---

## ORadio

单选框传值：

1. `value` 用于设置选中后 `modelValue` 的值
2. `modelValue` 的类型是 `string | number | boolean`，当选中后 `modelValue` 的值为 `value` 值

单选框组：当单选框的数量较多时，单选框组可以用来简化 `v-model` 的书写，此时将 `v-model` 写在单选框组上即可

### 示例代码

```vue
<div class="demo-radio-usage-wrap">
  <ORadio class="demo-radio-usage" v-model="ctx.radioVal"  >Apple</ORadio>
    <div class="demo-radio-val">
    Selected：{{ ctx.radioVal }}
  </div></div>
```

> 详细使用说明和完整属性列表，请查看 [references/radio.md](references/radio.md)


---

## ORate




---

## OResult

1. `status` 控制展示结果的状态，有四种状态：`info`, `success`, `warning`, `danger`；
2. `title` 属性用于自定义结果展示的标题；
3. `description` 属性用于自定义对结果的补充描述；

### 示例代码

```vue
<div class="demo-result-usage-wrap">
  <OResult class="demo-result-usage"  />
   </div>
```

> 详细使用说明和完整属性列表，请查看 [references/result.md](references/result.md)


---

## OScrollbar

两种尺寸：`medium`、`small` ；

四种显示方式：`auto`、`always`、`hover`、`never` ；

滚动条显示方式为 `auto` 时,可以通过 `duration` 属性控制滚动条在停止滚动后持续显示的时间；

### 示例代码

```vue
<OScroller class="demo-scrollbar-usage-wrapper" >
        <div class="section">1</div>
        <div class="section">2</div>
        <div class="section">3</div>
      </OScroller>
```

> 详细使用说明和完整属性列表，请查看 [references/scrollbar.md](references/scrollbar.md)


---

## OSelect

输入框包含 `normal`、`success`、`warning`、`danger` 四种主题色；

三种尺寸：`small`、`medium`、`large` ；

三种形状：`solid`、`outline`、`text` ；

禁用状态：`disabled` ；

支持多选：`multiple` ；

选择框的圆角可以通过 `pill` 设置为半圆，也可以是 css 属性 `border-radius` 能够接受的其它值；

其他属性的说明请查看下方的 props 表。

### 示例代码

```vue
<div class="demo-select-usage-wrap">
  <OSelect v-model=ctx.selectedVal class="demo-select-usage" option-title="选项标题"   :max-tag-count="2">
   <OOption v-for="item in ctx.options" :key="item.value" :label="item.label" :value="item.value" />
  </OSelect>
   </div>
```

> 详细使用说明和完整属性列表，请查看 [references/select.md](references/select.md)


---

## OSkeleton

1. 骨架屏的显示与隐藏通过 `loading` 属性控制；
2. 骨架屏的动画效果通过 `animation` 属性控制；
3. 骨架屏的显示文本行数通过 `rows` 属性控制。

### 示例代码

```vue
<div class="demo-skeleton-usage-wrap">
            <OSkeleton   > Demo of Skeleton </OSkeleton>
          </div>
```

> 详细使用说明和完整属性列表，请查看 [references/skeleton.md](references/skeleton.md)


---

## OSwitch

两种种尺寸：`small`、`medium` ；

禁用切换：`disabled` ；

加载状态：`loading` ；

按钮的圆角可以通过 `pill` 设置为半圆，也可以是 css 属性 `border-radius` 能够接受的其它值；

可以通过 `checkedValue`、`uncheckedValue` 自定义选中状态与未选中状态对应的值。


---

## OTab




---

## OTable

OTable 是一个数据表格组件，用于展示结构化数据。

### 基础用法

OTable 通过 `columns` 和 `data` 属性来定义表格结构和数据：

```vue
<template>
  <OTable :columns="columns" :data="tableData" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTable } from '@opensig/opendesign'

// 定义列配置
const columns = [
  { key: 'name', label: '姓名' },
  { key: 'age', label: '年龄' },
  { key: 'email', label: '邮箱' },
  { key: 'status', label: '状态' }
]

// 定义表格数据
const tableData = ref([
  { name: '张三', age: 28, email: 'zhangsan@example.com', status: '活跃' },
  { name: '李四', age: 32, email: 'lisi@example.com', status: '活跃' },
  { name: '王五', age: 25, email: 'wangwu@example.com', status: '非活跃' }
])
</script>
```

### 列配置说明

每个列对象包含以下属性：
- `key`: 数据字段名（必需），对应 data 中每行对象的属性名
- `label`: 列标题（必需），显示在表头的文本

### 数据格式

`data` 属性接收一个对象数组，每个对象代表一行数据。对象的属性名应与 `columns` 中定义的 `key` 对应。

### 结合搜索和过滤

```vue
<template>
  <OInput v-model="searchText" placeholder="搜索..." />
  <OTable :columns="columns" :data="filteredData" />
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { OTable, OInput } from '@opensig/opendesign'

const searchText = ref('')

const columns = [
  { key: 'name', label: '姓名' },
  { key: 'email', label: '邮箱' }
]

const tableData = ref([
  { name: '张三', email: 'zhangsan@example.com' },
  { name: '李四', email: 'lisi@example.com' }
])

// 过滤数据
const filteredData = computed(() => {
  if (!searchText.value) return tableData.value
  return tableData.value.filter(item =>
    item.name.toLowerCase().includes(searchText.value.toLowerCase())
  )
})
</script>
```

### 插槽功能（重要）

**OTable 支持强大的插槽系统**，可以自定义单元格和表头内容！

#### 自定义单元格内容

使用 `#td_{columnKey}` 或 `#{columnKey}` 插槽自定义单元格：

```vue
<template>
  <OTable :columns="columns" :data="tableData">
    <!-- 自定义 name 列：添加链接 -->
    <template #td_name="{ row }">
      <router-link :to="`/detail/${row.id}`">{{ row.name }}</router-link>
    </template>

    <!-- 自定义 action 列：添加按钮 -->
    <template #action="{ row }">
      <OButton size="small" @click="handleEdit(row)">编辑</OButton>
      <OButton size="small" color="danger" @click="handleDelete(row)">删除</OButton>
    </template>
  </OTable>
</template>
```

#### 自定义表头

使用 `#th_{columnKey}` 插槽自定义表头，或使用 `#header` 插槽自定义整个表头（支持多行表头）：

```vue
<template>
  <OTable :columns="columnKeys" :data="tableData">
    <template #header>
      <tr>
        <th rowspan="2">姓名</th>
        <th colspan="3">详细信息</th>
      </tr>
      <tr>
        <th>工资</th>
        <th>地址</th>
        <th>邮箱</th>
      </tr>
    </template>
  </OTable>
</template>
```

### 其他高级功能

- **边框样式**：`border="all"` | `"row"` | `"column"` | `"row-column"` | `"row-frame"` | `"column-frame"`
- **小尺寸**：`small` 属性
- **加载状态**：`loading` 属性
- **空数据提示**：`empty-label` 属性
- **单元格合并**：`:cell-span` 函数
- **分页集成**：`:pagination` 对象 + `@change:page` 事件

### 完整示例：带下钻功能的表格

```vue
<template>
  <OTable :columns="columns" :data="tableData">
    <template #td_activityName="{ row }">
      <router-link :to="`/activity-detail?id=${row.id}`" class="activity-link">
        {{ row.activityName }}
      </router-link>
    </template>
  </OTable>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTable } from '@opensig/opendesign'

const columns = [
  { label: '社区', key: 'community' },
  { label: '活动名称', key: 'activityName' },
  { label: '时间', key: 'time' }
]

const tableData = ref([
  { id: 1, community: 'openEuler', activityName: 'Summit 2024', time: '2024-03-15' }
])
</script>

<style scoped>
.activity-link {
  color: rgb(0, 47, 167);
  text-decoration: none;
}
.activity-link:hover {
  opacity: 0.7;
  text-decoration: underline;
}
</style>
```

### 何时使用自定义 HTML table

虽然 OTable 功能强大，但在以下极少数情况下可能需要自定义 HTML table：
- 需要完全自定义的表格结构（OTable 无法满足）
- 需要特殊的样式或布局（超出 OTable 能力范围）

**推荐优先使用 OTable**，因为它提供了：
- 插槽系统（自定义单元格和表头）
- 内置加载状态和空数据处理
- 多种边框样式
- 单元格合并
- 分页集成
- 更简洁的代码

> 详细使用说明和完整属性列表，请查看 [references/table.md](references/table.md)

```vue
<template>
  <table class="custom-table">
    <thead>
      <tr>
        <th v-for="col in columns" :key="col.key">{{ col.label }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in tableData" :key="row.id">
        <td>
          <router-link :to="`/detail/${row.id}`">{{ row.name }}</router-link>
        </td>
        <td>{{ row.email }}</td>
        <td>
          <button @click="handleEdit(row)">编辑</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
.custom-table {
  width: 100%;
  border-collapse: collapse;
}

.custom-table thead {
  background-color: #f5f7fa;
}

.custom-table th {
  padding: 12px 16px;
  text-align: left;
  font-weight: 600;
  color: #333;
  border-bottom: 2px solid #e4e7ed;
}

.custom-table td {
  padding: 12px 16px;
  border-bottom: 1px solid #e4e7ed;
  color: #606266;
}

.custom-table tbody tr:hover {
  background-color: #f5f7fa;
}
</style>
```

### 使用建议

1. **简单数据展示** → 使用 OTable
   - 纯文本数据
   - 不需要自定义单元格内容
   - 快速实现表格功能

2. **复杂交互需求** → 使用自定义 HTML table
   - 需要添加链接、按钮等交互元素
   - 需要自定义单元格样式
   - 需要实现下钻、编辑等功能

> 详细使用说明和完整属性列表，请查看 [references/table.md](references/table.md)


---

## OTag

<!-- en US -->

## Usage


---

## OTextarea



### 示例代码

```vue
<OTextarea  v-model="ctx.modelValue"/>
```

> 详细使用说明和完整属性列表，请查看 [references/textarea.md](references/textarea.md)


---

## OToggle

选择块是指示当前状态并提供切换操作的表单控件，并支持插槽以实现自定义显示。可设置项包含：

双向绑定状态 `checked`；

非受控状态时是否选中 `defaultChecked`；

圆角值 `round`；

前缀图标 `icon`；

是否禁用 `disabled`；

还可以配合 `ORadio`、`ORadioGroup` 等组件达到唯一选择的目的。


---

## OUpload

用于上传文件到服务端。可设置项包含：

MIME类型 `accept`；

是否禁用 `disabled`；

是否支持多选 `multiple`；

上传触发时机 `lazyUpload`；

拖拽上传 `draggable`；

文件列表类型 `listType`；

按钮文本 `btnLabel` 等。

### 示例代码

```vue
<OUpload
  v-model="ctx.singleFileList"
  
  :on-after-select="ctx.onAfterSelect"
  :upload-request="ctx.uploadRequest"
  color="normal"
  variant="solid"
/>
```

> 详细使用说明和完整属性列表，请查看 [references/upload.md](references/upload.md)


---

## OVirtualList



### 示例代码

```vue
<OVirtualList class="virtual-list-demo container"  :list="ctx.list">
  <template  #default="{ item, index }">
    <div :key="item.label" class="section" :class="\
```

> 详细使用说明和完整属性列表，请查看 [references/virtual-list.md](references/virtual-list.md)


---


## 更多信息

每个组件的详细使用说明和完整属性列表，请查看 `references/` 目录下对应的组件文档。

## 常用组合模式

### 表单页面
使用 `OForm` + `OFormItem` + `OInput`/`OSelect`/`OTextarea` 等构建表单。

### 数据展示
使用 `OTable` 展示表格数据，`OCard` 展示卡片信息。

### 交互反馈
使用 `ODialog` 显示对话框，`OMessage` 显示消息提示，`OLoading` 显示加载状态。

