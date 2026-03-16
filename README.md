# OpenDesign Skills

OpenDesign 生态的 AI Skill 集合，为 AI 编码助手提供 OpenDesign 组件库、构建工具、设计令牌和前端开发规范的完整知识。

---

## Skill 总览

| Skill | 包名 | 覆盖范围 | 参考文件数 |
|-------|------|---------|-----------|
| [opendesign-components](#opendesign-components) | `@opensig/opendesign` | 46 个 Vue 3 UI 组件 | 46 |
| [opendesign-scripts](#opendesign-scripts) | `@opensig/open-scripts` | 5 个 CLI 构建命令 | 5 |
| [opendesign-tokens](#opendesign-tokens) | `@opensig/opendesign-token` | 3 套主题的设计令牌体系 | 4 |
| [openeuler-frontend-tools](#openeuler-frontend-tools) | — | Composables / Mixins / Utils | 3 |

---

## opendesign-components

**用途**：使用 OpenDesign Vue 3 组件库构建页面时加载此 skill。

**适用场景**：
- 使用 OpenDesign 组件搭建 Vue 页面
- 查找组件 API（props / events / slots / expose）
- 获取组件代码示例和最佳实践

**覆盖 46 个组件**（按字母序）：

| 组件 | 说明 | 组件 | 说明 |
|------|------|------|------|
| Anchor | 锚点导航 | Link | 链接 |
| Badge | 徽标 | Loading | 加载遮罩 |
| Breadcrumb | 面包屑 | Menu | 导航菜单 |
| Button | 按钮 | Message | 全局消息 |
| Card | 卡片 | Pagination | 分页 |
| Carousel | 轮播 | Popover | 气泡卡片 |
| Cascader | 级联选择 | Popup | 弹出层 |
| Checkbox | 复选框（含 Group） | Progress | 进度条 |
| Collapse | 折叠面板 | Radio | 单选框（含 Group） |
| ConfigProvider | 全局配置 | Rate | 评分 |
| DataTable | 数据表格 | Result | 结果页 |
| Dialog | 对话框 | Scrollbar | 滚动条 |
| Divider | 分割线 | Select | 下拉选择（含 OptionGroup） |
| Dropdown | 下拉菜单 | Skeleton | 骨架屏 |
| Figure | 图片 | Slider | 滑块 |
| Form | 表单（含 FormItem） | Step | 步骤条 |
| Grid | 栅格布局 | Switch | 开关 |
| Icon | 图标 | Tab | 标签页 |
| Input | 输入框 | Tag | 标签 |
| InputNumber | 数字输入框 | Textarea | 文本域 |
| IpInput | IP 地址输入框 | Toast | 轻提示 |
| Layer | 浮层基础组件 | Toggle | 切换按钮 |
| — | — | Upload | 上传 |
| — | — | VirtualList | 虚拟列表 |

> 跳过：OTable（按规则不生成 skill）

**目录结构**：
```
skills/opendesign-components/
├── SKILL.md                          # 主 skill 文件（含安装指南和组件索引）
└── references/
    └── {component}.md                # 各组件的 skill 文件（×46）
```

---

## opendesign-scripts

**用途**：使用 `@opensig/open-scripts` CLI 工具进行构建、图标生成、样式编译时加载此 skill。

**适用场景**：
- 配置和执行构建脚本
- 编写图标 / 令牌配置文件
- 了解构建流程和命令依赖关系

**覆盖 5 个命令**：

| 命令 | 说明 | 适用项目 |
|------|------|---------|
| `gen:icon` | 从 SVG 文件生成 Vue 图标组件 | 组件库 + 业务项目 |
| `clean:svg` | 清理和优化 SVG 文件 | 组件库 + 业务项目 |
| `build:component` | 构建 Vue 组件库（ESM/CJS/UMD） | 仅组件库开发 |
| `build:style` | 编译 SCSS 样式为 CSS | 仅组件库开发 |
| `gen:token` | 从 JSON 生成设计令牌 CSS 变量 | 仅令牌包构建 |

**标准构建流程**：`clean:svg → gen:icon → build:component → build:style`

**目录结构**：
```
skills/opendesign-scripts/
├── SKILL.md                          # 主 skill 文件（含安装指南和命令详解）
└── references/
    └── {command}.md                  # 各命令的 skill 文件（×5）
```

---

## opendesign-tokens

**用途**：在代码中使用 `@opensig/opendesign-token` 的 CSS 变量（设计令牌）时加载此 skill。

**适用场景**：
- 查找颜色值对应的语义 token 名称
- 获取间距 / 圆角 / 字体的 token
- 了解三套主题（openEuler / Ascend / Kunpeng）的差异
- 用 CSS 变量替代硬编码值

**Token 体系**：
```
基础 Token（调色板）  →  语义 Token（颜色意义）  →  组件级 Token
--o-kleinblue-6      →  --o-color-primary1      →  --btn-color
```

**三套主题**：

| 主题 | 社区 | 品牌色 | 引入文件前缀 |
|------|------|--------|------------|
| `e` | openEuler | Klein Blue | `e.light.token.css` / `e.dark.token.css` |
| `a` | Ascend | Ascend 品牌色 | `a.light.token.css` / `a.dark.token.css` |
| `k` | Kunpeng | Kunpeng 品牌色 | `k.light.token.css` / `k.dark.token.css` |

**目录结构**：
```
skills/opendesign-tokens/
├── SKILL.md                          # 主 skill 文件（含 token 体系说明）
├── scripts/
│   └── convert_to_token.py           # Token 转换脚本
└── references/
    ├── tokens.md                     # 通用 token 参考
    ├── tokens-openeuler.md           # openEuler 主题 token
    ├── tokens-ascend.md              # Ascend 主题 token
    └── tokens-kunpeng.md             # Kunpeng 主题 token
```

---

## openeuler-frontend-tools

**用途**：在 openEuler Portal 项目中使用通用 composables、SCSS mixins 或工具函数时加载此 skill。

**适用场景**：
- 响应式屏幕适配（`useScreen`）
- 响应式字体 mixin（`font.scss`）
- URL 参数 / Cookie / 国际化等工具函数

**工具分类**：

| 分类 | 内容 | 参考文件 |
|------|------|---------|
| Composables | useScreen、useLocale、useClipboard、useDebounceSearch、useCheckbox、useScrollBottom、useInViewDuration | `composables.md` |
| SCSS Mixins | screen.scss（断点）、font.scss（响应式字体）、common.scss（暗色模式、截断、滚动条） | `mixins.md` |
| Utils | URL 参数、Cookie、时间格式化、Git 平台检测、语言环境 | `utils.md` |

**目录结构**：
```
skills/openeuler-frontend-tools/
├── SKILL.md                          # 主 skill 文件
└── references/
    ├── composables.md                # Vue 组合式函数参考
    ├── mixins.md                     # SCSS 混入参考
    └── utils.md                      # 工具函数参考
```

---

## Skill 之间的关系

```
opendesign-tokens          opendesign-scripts
(设计令牌 CSS 变量)         (CLI 构建工具)
       │                        │
       │ 提供主题变量             │ gen:icon 生成图标组件
       │ 供组件消费               │ build:component 构建产物
       ▼                        ▼
opendesign-components ◄─────────┘
(46 个 Vue 3 UI 组件)
       │
       │ 被业务项目使用
       ▼
openeuler-frontend-tools
(Portal 项目的通用工具)
```

**业务项目的典型使用路径**：
1. 安装 `@opensig/opendesign` + `@opensig/opendesign-token`
2. 选择主题，引入 token CSS（参考 **opendesign-tokens**）
3. 使用组件搭建页面（参考 **opendesign-components**）
4. 如有自定义图标，使用 `gen:icon`（参考 **opendesign-scripts**）
5. 使用项目通用工具（参考 **openeuler-frontend-tools**）

---

## 统计

| 指标 | 数量 |
|------|------|
| Skill 大类 | 4 |
| 组件 Skill | 46 |
| 脚本 Skill | 5 |
| Token 参考 | 4 |
| 工具参考 | 3 |
| 参考文件总计 | 58 |
