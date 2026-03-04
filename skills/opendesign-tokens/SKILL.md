---
name: opendesign-tokens
description: OpenEuler 设计 Token 转换工具。当需要将设计稿中的颜色、尺寸、字体等属性值转换为对应的 CSS token 变量时使用此 skill。支持自动识别设计稿中的颜色值（十六进制、RGB）、尺寸值、字体值等，并转换为对应的 token 变量。使用场景：(1) 从设计稿生成代码时自动替换为 token，(2) 查找设计值对应的 token 名称，(3) 批量转换设计稿属性值
---

# OpenEuler 设计 Token 转换指南

本 skill 帮助将设计稿中的属性值（颜色、尺寸、字体等）自动转换为对应的 CSS token 变量。

## Token 文件位置

项目中的 token 定义在以下文件中：
- **Light 主题**: `openEuler-portal/app/.vitepress/src-new/assets/style/theme/default-light.token.css`
- **Dark 主题**: `openEuler-portal/app/.vitepress/src-new/assets/style/theme/dark.token.css`

设计稿通常以 **light 主题** 呈现。

## Token 体系

### 基础 Token vs 语义 Token

#### 基础 Token（Base Tokens）
基础 token 是调色板颜色，用于服务语义 token，**不应直接在代码中使用**：

```css
/* 基础 token - 不要直接使用 */
--o-white: 255, 255, 255;
--o-black: 0, 0, 0;
--o-kleinblue-1: 235, 241, 250;
--o-kleinblue-6: 0, 47, 167;  /* light 主题 */
--o-kleinblue-6: 73, 122, 248; /* dark 主题 */
```

#### 语义 Token（Semantic Tokens）
语义 token 具有明确的使用场景，**支持 light/dark 主题自动切换**，应优先使用：

```css
/* 语义 token - 推荐使用 */
--o-color-primary1: rgb(var(--o-kleinblue-6));
/* light 主题：rgb(0, 47, 167) */
/* dark 主题：rgb(73, 122, 248) */

--o-color-fill1: rgb(var(--o-mixedgray-2));
/* light 主题：rgb(243, 243, 245) - 页面背景 */
/* dark 主题：rgb(26, 26, 28) - 页面背景 */
```

## 快速开始

### 转换颜色值（优先使用语义化 Token）

设计稿中的颜色值会自动转换为**语义化 token**，这些 token 会根据主题（light/dark）自动切换：

```css
/* 设计稿值 */
color: #002FA7;
background: rgb(0, 47, 167);

/* 转换为语义化 token（推荐） */
color: var(--o-color-primary1);
background: var(--o-color-primary1);

/* 语义化 token 的优势：
 * - 在 light 主题下：--o-color-primary1 = rgb(0, 47, 167)
 * - 在 dark 主题下：--o-color-primary1 = rgb(73, 122, 248)
 * - 自动适配主题，无需手动切换
 */
```

### 转换尺寸值

设计稿中的尺寸值可以自动转换为 token：

```css
/* 设计稿值 */
border-radius: 8px;
gap: 16px;
padding: 24px;

/* 转换为 token */
border-radius: var(--o-radius-s);
gap: var(--o-gap-4);
padding: var(--o-gap-5);
```

## 使用方法

### 方法 1: 使用转换脚本

运行转换脚本进行自动转换：

```bash
python scripts/convert_to_token.py "#002FA7"
# 输出: var(--o-color-primary1)  ✅ 语义化 token

python scripts/convert_to_token.py "rgb(0, 47, 167)"
# 输出: var(--o-color-primary1)  ✅ 语义化 token

python scripts/convert_to_token.py "8px"
# 输出: var(--o-radius-s)  或  var(--o-gap-2)
```

### 方法 2: 手动查找

查看 [references/tokens.md](references/tokens.md) 查找对应的 token。

## Token 类型详解

### 1. 颜色 Token

#### 语义化颜色（推荐使用）

**主色系：**
- `--o-color-primary1` - 主色（常规）
- `--o-color-primary2` - 主色（悬浮）
- `--o-color-primary3` - 主色（激活）
- `--o-color-primary4` - 主色（禁用）

**状态色：**
- `--o-color-success1` - 成功色（常规）
- `--o-color-success2/3/4` - 成功色（其他状态）
- `--o-color-warning1` - 警告色（常规）
- `--o-color-warning2/3/4` - 警告色（其他状态）
- `--o-color-danger1` - 危险色（常规）
- `--o-color-danger2/3/4` - 危险色（其他状态）

**信息色（文本颜色）：**
- `--o-color-info1` - 一级/强调/标题
- `--o-color-info2` - 二级/次强调/正文
- `--o-color-info3` - 三级/辅助信息
- `--o-color-info4` - 四级/禁用文本

**填充色（背景色）：**
- `--o-color-fill1` - 一级填充：页面背景
- `--o-color-fill2` - 二级填充：区块/卡片（**最常用**）
- `--o-color-fill3` - 三级填充：嵌套卡片

**控件色：**
- `--o-color-control1` - 控件色（常规），常用于边框
- `--o-color-control2/3/4` - 控件色（其他状态）

**链接色：**
- `--o-color-link1` - 链接色（常规）
- `--o-color-link2/3/4` - 链接色（其他状态）

**遮罩色：**
- `--o-color-mask1` - 遮罩色（深）
- `--o-color-mask2` - 遮罩色（浅）

**基础色：**
- `--o-color-white` - 纯白色（极少使用）
- `--o-color-black` - 纯黑色（极少使用）

### 2. 间距 Token（gap 系列）

```css
--o-gap-1: 4px;   /* 最小间距 */
--o-gap-2: 8px;   /* 小间距 */
--o-gap-3: 12px;  /* 中小间距 */
--o-gap-4: 16px;  /* 常规间距 */
--o-gap-5: 24px;  /* 中等间距 */
--o-gap-6: 32px;  /* 大间距 */
--o-gap-7: 40px;  /* 较大间距 */
--o-gap-8: 48px;  /* 很大间距 */
--o-gap-9: 64px;  /* 超大间距 */
--o-gap-10: 72px; /* 最大间距 */
```

**使用场景：**
- `gap` 属性：flex/grid 布局的间距
- `padding` 属性：内边距
- `margin` 属性：外边距

### 3. 圆角 Token（radius 系列）

```css
--o-radius-xs: 4px;   /* 超小圆角 */
--o-radius-s: 8px;    /* 小圆角 */
--o-radius-m: 12px;   /* 中等圆角 */
--o-radius-l: 16px;   /* 大圆角 */
--o-radius-xl: 24px;  /* 超大圆角 */
```

**控件圆角（用于按钮、输入框等）：**
```css
--o-radius_control-xs: 4px;
--o-radius_control-s: 8px;
--o-radius_control-m: 12px;
--o-radius_control-l: 16px;
```

### 4. 字体 Token

#### 字体大小（font_size 系列）

```css
--o-font_size-tip1: 14px;    /* 提示文本1 */
--o-font_size-tip2: 12px;    /* 提示文本2 */
--o-font_size-text1: 16px;   /* 常规正文 */
--o-font_size-text2: 18px;   /* 大号正文 */
--o-font_size-h4: 20px;      /* 四级标题 */
--o-font_size-h3: 22px;      /* 三级标题 */
--o-font_size-h2: 24px;      /* 二级标题 */
--o-font_size-h1: 32px;      /* 一级标题 */
--o-font_size-display1: 56px; /* 展示文本1 */
--o-font_size-display2: 48px; /* 展示文本2 */
--o-font_size-display3: 40px; /* 展示文本3 */
```

#### 行高（line_height 系列）

```css
--o-line_height-tip1: 22px;   /* 提示文本1行高 */
--o-line_height-tip2: 18px;   /* 提示文本2行高 */
--o-line_height-text1: 24px;  /* 正文行高 */
--o-line_height-text2: 26px;  /* 大号正文行高 */
--o-line_height-h4: 28px;     /* 四级标题行高 */
--o-line_height-h3: 30px;     /* 三级标题行高 */
--o-line_height-h2: 32px;     /* 二级标题行高 */
--o-line_height-h1: 44px;     /* 一级标题行高 */
--o-line_height-display1: 80px; /* 展示文本1行高 */
--o-line_height-display2: 64px; /* 展示文本2行高 */
--o-line_height-display3: 56px; /* 展示文本3行高 */
```

**使用建议：**
- 字体大小和行高应配套使用
- 例如：`font-size: var(--o-font_size-h3); line-height: var(--o-line_height-h3);`

### 5. 阴影 Token（shadow 系列）

```css
--o-shadow-1: 0 3px 8px rgba(var(--o-mixedgray-9), 0.08);   /* 卡片、小弹窗、楼层阴影 */
--o-shadow-2: 0 2px 24px rgba(var(--o-mixedgray-9), 0.15); /* 卡片悬浮阴影 */
--o-shadow-3: 0 8px 40px rgba(var(--o-mixedgray-9), 0.1);  /* 大弹窗、抽屉阴影 */
```

**使用场景：**
- `--o-shadow-1`：默认卡片阴影
- `--o-shadow-2`：悬浮状态阴影
- `--o-shadow-3`：模态框、抽屉等大型浮层阴影

### 6. 动画 Token

#### 持续时间（duration 系列）

```css
--o-duration-s: 200ms;    /* 短动画 */
--o-duration-m1: 250ms;   /* 中等动画1 */
--o-duration-m2: 300ms;   /* 中等动画2 */
--o-duration-m3: 400ms;   /* 中等动画3 */
--o-duration-l: 500ms;    /* 长动画 */
--o-duration-xl: 1000ms;  /* 超长动画 */
```

#### 缓动曲线（easing 系列）

```css
--o-easing-linear: cubic-bezier(0, 0, 1, 1);           /* 线性 */
--o-easing-standard: cubic-bezier(0.2, 0, 0, 1);       /* 标准（推荐） */
--o-easing-standard-in: cubic-bezier(0, 0, 0, 1);      /* 标准进入 */
--o-easing-standard-out: cubic-bezier(0.3, 0, 1, 1);   /* 标准退出 */
--o-easing-emphasized: cubic-bezier(0.2, 0, 0, 1);     /* 强调 */
--o-easing-emphasized-in: cubic-bezier(0.3, 0, 0.8, 0.15); /* 强调进入 */
--o-easing-emphasized-out: cubic-bezier(0.05, 0.7, 0.1, 1); /* 强调退出 */
```

**使用示例：**
```css
transition: all var(--o-duration-m1) var(--o-easing-standard);
```

### 7. 控件尺寸 Token（control_size 系列）

```css
--o-control_size-2xs: 14px;  /* 超超小控件 */
--o-control_size-xs: 16px;   /* 超小控件 */
--o-control_size-s: 24px;    /* 小控件 */
--o-control_size-m: 32px;    /* 中等控件 */
--o-control_size-l: 40px;    /* 大控件 */
--o-control_size-xl: 48px;   /* 超大控件 */
--o-control_size-2xl: 56px;  /* 超超大控件 */
```

### 8. 图标尺寸 Token（icon_size 系列）

```css
--o-icon_size-xs: 16px;   /* 超小图标 */
--o-icon_size-s: 20px;    /* 小图标 */
--o-icon_size-m: 24px;    /* 中等图标 */
--o-icon_size-l: 32px;    /* 大图标 */
--o-icon_size-xl: 40px;   /* 超大图标 */
--o-icon_size-2xl: 48px;  /* 超超大图标 */
--o-icon_size-3xl: 56px;  /* 超超超大图标 */
--o-icon_size-4xl: 64px;  /* 最大图标 */
```

## 转换规则

### 颜色转换（优先语义化 Token）

转换工具会**优先使用语义化 token**，这些 token 以 `--o-color-` 开头，能够自动适配 light/dark 主题：

1. **十六进制颜色**: `#002FA7` → `var(--o-color-primary1)` ✅ 语义化 token
2. **RGB 颜色**: `rgb(0, 47, 167)` → `var(--o-color-primary1)` ✅ 语义化 token
3. **RGBA 颜色**: `rgba(0, 47, 167, 0.8)` → `var(--o-color-primary1)` (注意：透明度需要单独处理)

**为什么使用语义化 token？**
- ✅ **自动主题切换**：同一个 token 在 light/dark 主题下使用不同的基础颜色值
- ✅ **语义清晰**：`--o-color-primary1` 比 `--o-kleinblue-6` 更易理解
- ✅ **维护方便**：修改主题时只需更新 token 定义，无需修改代码

### 尺寸转换

1. **精确匹配**: 如果设计稿中的值与 token 值完全匹配，直接转换
2. **多个匹配**: 某些值可能对应多个 token（如 `12px` 可以是 `gap-3`、`radius-m` 等），根据使用场景选择：
   - 用于间距 → `--o-gap-3`
   - 用于圆角 → `--o-radius-m`
   - 用于字体 → `--o-font_size-tip2`

### 背景色转换（重要）

**设计稿中的白色背景应优先转换为语义化填充色 token：**

```css
/* 设计稿值 */
background-color: #FFFFFF;
background-color: rgb(255, 255, 255);

/* ❌ 不推荐：直接使用白色 token */
background-color: var(--o-color-white);

/* ✅ 推荐：根据使用场景选择语义化填充色 */
/* 如果是卡片/区块背景 */
background-color: var(--o-color-fill2); /* 二级填充：区块/卡片 */

/* 如果是页面背景 */
background-color: var(--o-color-fill1); /* 一级填充：页面背景 */
```

**转换规则：**
1. **页面背景** → `var(--o-color-fill1)`
2. **卡片/区块背景** → `var(--o-color-fill2)`（最常用）
3. **嵌套卡片背景** → `var(--o-color-fill3)`
4. **特殊场景需要纯白色** → `var(--o-color-white)`（极少使用）

## 使用场景对照表

### 背景色使用场景

| 使用场景 | 推荐 Token | 说明 |
|---------|-----------|------|
| 页面背景 | `--o-color-fill1` | 一级填充：页面背景 |
| 卡片/区块背景 | `--o-color-fill2` | 二级填充：区块/卡片（**最常用**） |
| 嵌套卡片背景 | `--o-color-fill3` | 三级填充：卡片 |
| 需要纯白色（特殊场景） | `--o-color-white` | 仅在确实需要纯白色时使用 |

### 文本颜色使用场景

| 使用场景 | 推荐 Token | 说明 |
|---------|-----------|------|
| 标题/强调文本 | `--o-color-info1` | 一级信息色 |
| 正文 | `--o-color-info2` | 二级信息色 |
| 辅助信息 | `--o-color-info3` | 三级信息色 |
| 禁用文本 | `--o-color-info4` | 四级信息色 |

### 间距使用场景

| 使用场景 | 推荐 Token | 值 |
|---------|-----------|-----|
| 最小间距（紧凑布局） | `--o-gap-1` | 4px |
| 小间距（组件内部） | `--o-gap-2` | 8px |
| 中小间距（相关元素） | `--o-gap-3` | 12px |
| 常规间距（默认） | `--o-gap-4` | 16px |
| 中等间距（区块间） | `--o-gap-5` | 24px |
| 大间距（页面布局） | `--o-gap-6` | 32px |

## 工作流程

1. **提取设计稿值**: 从设计稿（Pixso、Figma、Sketch 等）中提取颜色、尺寸等属性值
2. **运行转换**: 使用转换脚本或手动查找对应的 token
3. **替换代码**: 在生成的代码中使用 token 变量替代硬编码的值
4. **验证**: 确保转换后的 token 在 light 和 dark 主题下都正确显示

## 最佳实践

### ✅ 推荐做法

```css
/* 使用语义化 token */
.card {
  background-color: var(--o-color-fill2);
  border: 1px solid var(--o-color-control1);
  border-radius: var(--o-radius-m);
  padding: var(--o-gap-4);
  gap: var(--o-gap-3);
  box-shadow: var(--o-shadow-1);
}

.title {
  font-size: var(--o-font_size-h3);
  line-height: var(--o-line_height-h3);
  color: var(--o-color-info1);
}

.button:hover {
  transition: all var(--o-duration-m1) var(--o-easing-standard);
  box-shadow: var(--o-shadow-2);
}
```

### ❌ 不推荐做法

```css
/* 不要直接使用基础 token */
.card {
  background-color: rgb(var(--o-white)); /* ❌ 应使用 var(--o-color-fill2) */
  border: 1px solid rgb(var(--o-mixedgray-5)); /* ❌ 应使用 var(--o-color-control1) */
}

/* 不要硬编码值 */
.card {
  padding: 16px; /* ❌ 应使用 var(--o-gap-4) */
  border-radius: 12px; /* ❌ 应使用 var(--o-radius-m) */
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.08); /* ❌ 应使用 var(--o-shadow-1) */
}

/* 不要使用不存在的 token */
.card {
  padding: var(--o-spacing-m); /* ❌ 不存在，应使用 var(--o-gap-4) */
}
```

## 注意事项

- 转换工具会**自动优先选择语义化 token**
- 如果找不到匹配的语义化 token，会回退到基础 token
- 某些值可能对应多个 token，根据使用场景选择合适的 token
- 如果找不到匹配的 token，可能需要添加新的 token 或使用最接近的值
- **不要直接使用基础 token**（如 `--o-kleinblue-6`），应使用语义 token（如 `--o-color-primary1`）

## 参考文档

- [完整 Token 列表](references/tokens.md) - 所有可用的 token 及其值
- [转换脚本](scripts/convert_to_token.py) - 自动转换工具
- [Light 主题 Token](../../openEuler-portal/app/.vitepress/src-new/assets/style/theme/default-light.token.css) - Light 主题 token 定义
- [Dark 主题 Token](../../openEuler-portal/app/.vitepress/src-new/assets/style/theme/dark.token.css) - Dark 主题 token 定义
