# OpenDesign Skill 全局约定

本文件定义所有 skill 文件共同遵守的约定，各 skill 文件只记录**与约定不同的例外情况**，无需重复说明。

---

## 组件命名

- 所有组件均以 `O` 前缀命名（如 `OButton`、`OInput`）
- 从 `@opensig/opendesign` 统一导入

---

## 响应式断点标准

opendesign 生态涉及两套断点体系，使用时注意区分：

### opendesign 组件库断点（isPhonePad 体系）

组件库运行时通过 `useScreen()` 检测，三个关键阈值：

| 条件 | 阈值 | 含义 |
|------|------|------|
| `isPhonePadSize` | **≤840px** ★ | 触控设备竖屏（手机 + 平板竖屏），组件布局发生主要变化 |
| `isPhonePad` | **≤1200px** ★ | 所有触控/平板设备，UI 切换为紧凑模式 |
| 宽屏阈值 | **>1680px** ★ | 大屏/宽屏，部分组件有额外的宽屏布局 |

> ★ 这三个是组件库中**最关键**的响应式阈值，840 / 1200 / 1680 是核心边界。

**组件 skill 响应式行为表标准格式**（6 列，高亮关键阈值）：

| 维度 | ≤600px | **601–840px** ★ | **841–1200px** ★ | 1201–1680px ★ | >1680px |
|------|--------|----------------|-----------------|--------------|--------|
| （示例行） | — | — | — | — | — |

> 说明：
> - `≤600px`（纯手机）与 `601–840px`（平板竖屏）通常行为相同，opendesign 以 840px 为第一阈值
> - `1201–1680px` 为标准桌面，`>1680px` 为宽屏——部分组件在宽屏下有专属布局变化
> - `★` 标注的三列是组件行为发生实质变化的关键阈值
> - 若某行在某列无变化，填 `同前` 或重复当前值，不留空

---

### openEuler Portal 项目断点（screen.scss 体系）

Portal 项目通过 `@include respond-to('xxx')` 使用，断点定义：

| 名称 | 范围 | 说明 |
|------|------|------|
| `phone` | 0–600px | 手机 |
| `pad_v` | 601–840px | 平板竖屏 |
| `pad_h` | 841–1200px | 平板横屏 |
| `pad` | 601–1200px | 全部平板（pad_v + pad_h） |
| `laptop` | 1201–1440px | 笔记本 |
| `<=pad` | 0–1200px | 平板及以下 |
| `<=laptop` | 0–1440px | 笔记本及以下 |
| `>pad` | ≥1201px | 桌面及以上 |
| `pad-laptop` | 601–1440px | 平板 + 笔记本 |

---

## Slot 渲染约定

- slot 未传入时，组件**不渲染**对应区域（除非该 skill 文件另有说明）
- 外层 slot 被使用时，内部所有子 slot **全部失效**（另有说明除外）

---

## 触控 vs 指针设备

通过 `isTouchDevice` 检测：

| 设备类型 | 说明 | 影响 |
|---------|------|------|
| 触控设备（`isTouchDevice=true`） | 手机、平板 | hover 交互退化为 click；部分弹出层行为改变 |
| 指针设备（`isTouchDevice=false`） | 桌面鼠标 | 完整 hover 效果；tooltip 等 hover 触发组件正常工作 |

---

## 组件 CSS 变量覆盖

所有组件均支持在调用处直接覆盖 CSS 变量，**无需 `:deep` hack**：

```vue
<OButton style="--btn-min-width: 120px" />
```

各组件的可覆盖变量列表见各 skill 文件的「可覆盖的 CSS 变量」章节。

---

## 文件组织约定

### 文件层级

```
README.md                              ← 仓库入口索引
skills/
├── CONVENTIONS.md                     ← 本文件（全局约定）
├── opendesign-components/
│   ├── SKILL.md                       ← 组件库入口（安装、索引、Pixso 指南）
│   └── references/
│       └── {component}.md             ← 单个组件完整 skill（×46）
├── opendesign-scripts/
│   ├── SKILL.md                       ← 脚本工具入口
│   └── references/
│       └── {command}.md               ← 单个命令完整 skill（×5）
├── opendesign-tokens/
│   ├── SKILL.md                       ← Token 体系入口
│   └── references/
│       └── tokens-{theme}.md          ← 各主题 token 参考（×7）
└── openeuler-frontend-tools/
    ├── SKILL.md                       ← 工具入口
    └── references/
        └── {tool}.md                  ← 工具参考（×3）
```

### 文件夹 vs 单文件

**当前采用平铺结构**（每个组件/命令一个 `.md` 文件），原因：
- 每个组件只有一个 skill 文件（review 文件已在 `.gitignore` 中排除，不进仓库）
- 平铺结构更适合直接链接和 RAG 按文件检索
- 若未来需要为单个组件添加多个文件（如 `.detail.md`），再按需引入文件夹结构

---

## 导航约定

所有 reference 文件头部均包含返回链接：
```
> ← [组件索引](../SKILL.md#组件索引) · [README](../../../README.md)
```
