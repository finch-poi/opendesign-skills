# OFigure

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

## 导入方式

```vue
<script setup>
import { OFigure } from '@opensig/opendesign';
</script>
```

