---
name: svg-line-icons
description: 统一风格 SVG 线条图标生成与管理的全流程 Skill。基于 Feather Icons 设计语言（24×24 viewBox、stroke-width=2、stroke-linecap=round、stroke-linejoin=round），为 Web 项目提供视觉一致的图标系统，替代不一致的 emoji 或混合风格图标。触发：用户提到「图标」「icon」「SVG图标」「线条图标」「图标风格统一」「替换emoji」「图标不一致」。
---

# SVG 线条图标 · 统一生成 Skill

## 角色扮演规则

此 Skill 激活后，我以"图标系统工程师"的方式工作：
- 我会先做 **图标审计**（扫描项目中所有图标，识别不一致之处）。
- 我会严格遵循 **Feather Icons 设计规范** 生成所有图标。
- 我会 **先输出 1 个 MVP 图标**，用户确认风格后再批量生成。
- 我会确保 **同一项目内所有图标视觉一致**（笔画、圆角、比例、颜色继承方式）。
- 我不会使用 emoji 作为图标，不会混用不同风格的图标库。

退出角色：用户说「退出」「切回正常」「不用扮演了」。

---

## 一、为什么需要这个 Skill

### 1.1 常见图标一致性问题

| 问题 | 症状 | 影响 |
|------|------|------|
| **Emoji 混用** | 🤖📦💻🔧📊🧠 与 SVG 图标共存 | 风格割裂、跨平台渲染不一致 |
| **多库混用** | Font Awesome + Material + 自绘 SVG 混搭 | 笔画粗细、圆角、比例不统一 |
| **尺寸不一** | 有的 16px 有的 24px 有的 1.5rem | 布局对齐困难 |
| **颜色硬编码** | 图标内 `fill="#333"` 而非 `currentColor` | 无法跟随主题切换 |
| **品牌图标缺失** | GitHub/LinkedIn 用 emoji 或文字替代 | 不专业、辨识度低 |

### 1.2 本 Skill 的核心价值

- **一致性**：所有图标遵循同一设计语言，视觉统一
- **可维护性**：通过 CSS `currentColor` 继承颜色，一处修改全局生效
- **跨平台**：SVG 矢量图标在任何分辨率下都清晰
- **轻量**：内联 SVG 无需额外网络请求，比图标字体更灵活

---

## 二、设计规范（Feather Icons 语言）

### 2.1 核心参数（铁律）

所有图标 **必须** 严格遵循以下参数：

```svg
<svg
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
  stroke-width="2"
  stroke-linecap="round"
  stroke-linejoin="round"
>
  <!-- 图标路径 -->
</svg>
```

| 参数 | 值 | 说明 |
|------|-----|------|
| `viewBox` | `0 0 24 24` | 固定 24×24 画布，通过 CSS 控制显示尺寸 |
| `fill` | `none` | 纯线条风格，不填充 |
| `stroke` | `currentColor` | 继承父元素文字颜色，支持主题切换 |
| `stroke-width` | `2` | 统一线条粗细 |
| `stroke-linecap` | `round` | 线条端点圆角 |
| `stroke-linejoin` | `round` | 线条交汇处圆角 |

### 2.2 品牌图标的特殊处理

品牌图标（GitHub、LinkedIn、Twitter 等）通常使用 **填充风格** 而非线条风格：

```svg
<!-- 品牌图标：使用 fill="currentColor"，无 stroke -->
<svg viewBox="0 0 24 24" fill="currentColor">
  <path d="M12 0c-6.626 0-12 5.373-12 12 ..."/>
</svg>
```

| 参数 | 线条图标 | 品牌图标 |
|------|---------|---------|
| `fill` | `none` | `currentColor` |
| `stroke` | `currentColor` | 不设置 |
| `stroke-width` | `2` | 不设置 |
| 来源 | Feather Icons / Lucide | Simple Icons / 官方 Logo |

### 2.3 CSS 集成规范

```css
/* 图标容器 */
.icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 24px;          /* 通过容器控制尺寸 */
  height: 24px;
  flex-shrink: 0;
  color: var(--accent); /* 颜色由 CSS 变量控制 */
}

.icon svg {
  width: 100%;
  height: 100%;
}

/* 不同尺寸变体 */
.icon-sm { width: 16px; height: 16px; }
.icon-lg { width: 32px; height: 32px; }
.icon-xl { width: 48px; height: 48px; }
```

### 2.4 JS 内联模板规范

在 JavaScript 中使用时，统一采用以下模板格式：

```javascript
const icons = {
  iconName: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="..."/></svg>`
};
```

**格式要求**：
- 单行字符串（便于在 JS 对象中阅读）
- 属性顺序：`viewBox` → `fill` → `stroke` → `stroke-width` → `stroke-linecap` → `stroke-linejoin`
- 路径紧凑排列，无多余空格

---

## 三、完整工作流（5 个阶段）

### Phase 1：图标审计

**目的**：扫描项目中所有图标，识别不一致之处

**审计清单**：

| 检查项 | 方法 | 工具 |
|--------|------|------|
| Emoji 图标 | 搜索 `[\x{1F300}-\x{1F9FF}]` Unicode 范围 | Grep |
| 外部图标字体引用 | 搜索 `font-awesome`、`material-icons` | Grep |
| 内联 SVG 风格 | 检查 `stroke-width`、`fill`、`viewBox` 一致性 | Grep + Read |
| 图标尺寸 | 检查 CSS 中图标容器的 `width/height` | Grep |
| 颜色继承方式 | 检查是否使用 `currentColor` | Grep |

**输出**：图标审计报告（不一致项清单 + 修复优先级）

### Phase 2：图标规划

**目的**：确定需要哪些图标，以及每个图标的语义

**规划表模板**：

| 图标名称 | 语义 | 类别 | 来源 | 备注 |
|---------|------|------|------|------|
| `phone` | 电话联系 | 通用 | Feather | 线条风格 |
| `github` | GitHub 链接 | 品牌 | Simple Icons | 填充风格 |
| `code` | 编程开发 | 技能 | Feather | 线条风格 |
| `brain` | 思维模型 | 技能 | Feather | 线条风格 |

**图标来源优先级**：
1. **Feather Icons / Lucide**（通用线条图标的首选）
2. **Simple Icons**（品牌图标的权威来源）
3. **自绘 SVG**（无现成图标时，遵循规范手绘）

### Phase 3：MVP 验证（1 个图标）

**目的**：先生成 1 个代表性图标，验证风格是否符合预期

**步骤**：
1. 选择一个最核心的图标（通常是 logo 或最显眼的功能图标）
2. 严格按 §2 规范生成 SVG
3. 集成到项目中实际预览
4. 验证以下质量门禁

**质量门禁**：
- [ ] `viewBox="0 0 24 24"` — 画布正确
- [ ] `fill="none"` — 纯线条（品牌图标除外）
- [ ] `stroke="currentColor"` — 颜色继承
- [ ] `stroke-width="2"` — 笔画一致
- [ ] `stroke-linecap="round"` — 端点圆角
- [ ] `stroke-linejoin="round"` — 交汇圆角
- [ ] 在 16px / 24px / 32px 三个尺寸下均清晰可辨
- [ ] 与文字并排时垂直居中对齐

**MVP 通过** → Phase 4
**MVP 不通过** → 调整后重新验证

### Phase 4：批量生成

**目的**：按规划表批量生成所有图标

**生成策略**：
- 优先从 Feather Icons / Lucide 图标库查找现成路径
- 品牌图标从 Simple Icons 获取
- 无现成图标时，基于规范手绘 SVG path

**输出格式**：根据集成方式选择

| 集成方式 | 输出格式 | 适用场景 |
|---------|---------|---------|
| **JS 内联对象** | `const icons = { ... }` | React/Vue/纯 JS 项目 |
| **独立 SVG 文件** | `icons/name.svg` | 需要按需加载或 sprite |
| **CSS Sprite** | `<symbol>` + `<use>` | 大型项目、需要按需引用 |

### Phase 5：集成与验收

**步骤**：
1. 将生成的图标集成到项目代码中
2. 统一 CSS 样式（容器尺寸、颜色继承）
3. 浏览器验证所有图标渲染效果
4. 检查暗色/亮色主题下的表现
5. 截图存档

---

## 四、常用图标速查库

### 4.1 通用线条图标（Feather Icons 风格）

#### 通讯 / 联系

| 名称 | SVG Path | 用途 |
|------|----------|------|
| phone | `<path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/>` | 电话 |
| mail | `<path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/>` | 邮箱 |
| send | `<line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/>` | 发送 |
| link | `<path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/>` | 链接 |
| globe | `<circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>` | 全球/网站 |

#### 开发 / 技术

| 名称 | SVG Path | 用途 |
|------|----------|------|
| code | `<polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/>` | 编程 |
| terminal | `<polyline points="4 17 10 11 4 5"/><line x1="12" y1="19" x2="20" y2="19"/>` | 终端 |
| git-branch | `<line x1="6" y1="3" x2="6" y2="15"/><circle cx="18" cy="6" r="3"/><circle cx="6" cy="18" r="3"/><path d="M18 9a9 9 0 0 1-9 9"/>` | Git 分支 |
| database | `<ellipse cx="12" cy="5" rx="9" ry="3"/><path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"/><path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/>` | 数据库 |
| cpu | `<rect x="4" y="4" width="16" height="16" rx="2" ry="2"/><rect x="9" y="9" width="6" height="6"/><line x1="9" y1="1" x2="9" y2="4"/><line x1="15" y1="1" x2="15" y2="4"/><line x1="9" y1="20" x2="9" y2="23"/><line x1="15" y1="20" x2="15" y2="23"/><line x1="20" y1="9" x2="23" y2="9"/><line x1="20" y1="14" x2="23" y2="14"/><line x1="1" y1="9" x2="4" y2="9"/><line x1="1" y1="14" x2="4" y2="14"/>` | 处理器 |

#### 产品 / 业务

| 名称 | SVG Path | 用途 |
|------|----------|------|
| package | `<path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/>` | 产品/模块 |
| layout | `<rect x="3" y="3" width="18" height="18" rx="2" ry="2"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="9" y1="21" x2="9" y2="9"/>` | 布局/设计 |
| bar-chart | `<line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/>` | 数据/图表 |
| target | `<circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/>` | 目标/质量 |
| tool | `<path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"/>` | 工具/工程 |

#### AI / 认知

| 名称 | SVG Path | 用途 |
|------|----------|------|
| bot | `<rect x="3" y="11" width="18" height="10" rx="2"/><circle cx="12" cy="5" r="3"/><path d="M8 15h0"/><path d="M16 15h0"/><path d="M9 18h6"/>` | AI/机器人 |
| brain | `<path d="M9.5 2A2.5 2.5 0 0 1 12 4.5v15a2.5 2.5 0 0 1-4.96.44 2.5 2.5 0 0 1-2.96-3.08 3 3 0 0 1-.34-5.58 2.5 2.5 0 0 1 1.32-4.24 2.5 2.5 0 0 1 4.44-1.5"/><path d="M14.5 2A2.5 2.5 0 0 0 12 4.5v15a2.5 2.5 0 0 0 4.96.44 2.5 2.5 0 0 0 2.96-3.08 3 3 0 0 0 .34-5.58 2.5 2.5 0 0 0-1.32-4.24 2.5 2.5 0 0 0-4.44-1.5"/>` | 思维/方法论 |
| zap | `<polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/>` | 能量/效率 |
| lightbulb | `<path d="M9 18h6"/><path d="M10 22h4"/><path d="M15.09 14c.18-.98.65-1.74 1.41-2.5A4.65 4.65 0 0 0 18 8 6 6 0 0 0 6 8c0 1 .23 2.23 1.5 3.5A4.61 4.61 0 0 1 8.91 14"/>` | 创意/想法 |

#### 生活 / 兴趣

| 名称 | SVG Path | 用途 |
|------|----------|------|
| camera | `<path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/><circle cx="12" cy="13" r="4"/>` | 摄影 |
| music | `<path d="M9 18V5l12-2v13"/><circle cx="6" cy="18" r="3"/><circle cx="18" cy="16" r="3"/>` | 音乐 |
| award | `<circle cx="12" cy="8" r="7"/><polyline points="8.21 13.89 7 23 12 20 17 23 15.79 13.88"/>` | 奖项/成就 |
| star | `<polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>` | 收藏/评分 |

### 4.2 品牌图标（填充风格）

| 名称 | SVG Path | 来源 |
|------|----------|------|
| github | `<path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>` | GitHub Octocat |
| linkedin | `<path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>` | LinkedIn |

---

## 五、自绘图标指南

当 Feather / Lucide / Simple Icons 中无现成图标时，需要手绘 SVG path。

### 5.1 自绘原则

1. **24×24 画布**：所有路径在 24×24 viewBox 内绘制
2. **2px 安全边距**：图标元素不超出 2~22 的范围（留出 stroke-width 的空间）
3. **几何优先**：优先使用 `<circle>`、`<rect>`、`<line>`、`<polyline>` 等基础图形
4. **对称设计**：图标尽量保持视觉对称或平衡
5. **最少元素**：用最少的路径表达清晰的语义

### 5.2 自绘流程

```
1. 确定语义 → 2. 搜索参考 → 3. 纸笔草图 → 4. SVG 编码 → 5. 多尺寸验证
```

### 5.3 常见语义 → 图标映射

| 语义 | 推荐图标 | 备选方案 |
|------|---------|---------|
| AI / 机器人 | `bot`（机器人头） | `cpu` + `zap` 组合 |
| 产品 / 模块 | `package`（3D 方块） | `box` |
| 编程 / 代码 | `code`（尖括号） | `terminal` |
| 工具 / 工程 | `tool`（扳手） | `settings` |
| 数据 / 图表 | `bar-chart`（柱状图） | `activity` |
| 思维 / 方法论 | `brain`（大脑） | `lightbulb` |
| 流程 / 自动化 | `git-branch`（分支） | `refresh-cw` |
| 质量 / 精度 | `target`（靶心） | `check-circle` |

---

## 六、质量门禁（Definition of Done）

### 6.1 单图标验收

- [ ] viewBox="0 0 24 24"
- [ ] fill="none"（品牌图标除外，用 fill="currentColor"）
- [ ] stroke="currentColor"
- [ ] stroke-width="2"
- [ ] stroke-linecap="round"
- [ ] stroke-linejoin="round"
- [ ] 16px 下可辨识
- [ ] 24px 下清晰
- [ ] 32px 下无锯齿
- [ ] 与文字并排时垂直居中

### 6.2 项目级验收

- [ ] 项目内无 emoji 图标
- [ ] 项目内无混用不同图标库风格
- [ ] 所有图标使用 currentColor 继承颜色
- [ ] 暗色主题下图标清晰可见
- [ ] 亮色主题下图标清晰可见
- [ ] 图标尺寸统一（通过 CSS 容器控制）

---

## 七、与相关 Skill 的分工

| 维度 | 本 Skill（svg-line-icons） | ai-image-generation | design-render |
|------|--------------------------|---------------------|---------------|
| **产出物** | SVG 矢量图标代码 | AI 生成的位图（JPG/PNG） | Python 绘制的渲染图 |
| **适用场景** | UI 图标、导航图标、功能图标 | 概念图、产品渲染、创意插图 | 封面图、数据图表风格化 |
| **一致性** | 100% 精确控制 | 概率性，每次略有不同 | 100% 精确控制 |
| **尺寸** | 任意缩放无损 | 固定分辨率 | 固定分辨率 |
| **颜色** | currentColor 动态继承 | 由 Prompt 决定 | 代码精确控制 |

**选择原则**：
- 需要 **UI 功能图标**（导航、按钮、标签） → 用本 Skill
- 需要 **照片级真实感图片** → 用 ai-image-generation
- 需要 **精确排版的项目封面** → 用 design-render

---

## 八、文件结构

```
svg-line-icons/
├── SKILL.md                    # 本文件（Skill 定义 + 全流程文档）
└── examples/                   # 范例文件
    ├── resume-icons-demo.html  # 完整集成范例（简历项目图标系统）
    └── icon-catalog.md         # 图标目录速查
```

---

## 九、实战范例：简历项目图标系统

### 9.1 场景描述

在简历网站项目中，需要将 Skills 部分的 emoji 图标（🤖📦💻🔧📊🧠）替换为统一的 SVG 线条图标，与 Contact 部分的联系方式图标风格保持一致。

### 9.2 图标映射表

| 原始 Emoji | 技能分类 | SVG 图标名称 | 语义 |
|-----------|---------|-------------|------|
| 🤖 | AI / Agent | `bot` | 机器人/AI |
| 📦 | 产品 / 数字化 | `package` | 产品/模块 |
| 💻 | 编程 / 开发 | `code` | 编程 |
| 🔧 | 工程 / 质量 | `tool` | 工具/工程 |
| 📊 | 数据 / 可视化 | `bar-chart` | 数据图表 |
| 🧠 | 方法论 / 思维模型 | `brain` | 思维/大脑 |

### 9.3 JS 集成代码

```javascript
const skillIcons = {
  'AI / Agent': `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="10" rx="2"/><circle cx="12" cy="5" r="3"/><path d="M8 15h0"/><path d="M16 15h0"/><path d="M9 18h6"/></svg>`,
  '产品 / 数字化': `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg>`,
  '编程 / 开发': `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>`,
  '工程 / 质量': `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"/></svg>`,
  '数据 / 可视化': `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg>`,
  '方法论 / 思维模型': `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9.5 2A2.5 2.5 0 0 1 12 4.5v15a2.5 2.5 0 0 1-4.96.44 2.5 2.5 0 0 1-2.96-3.08 3 3 0 0 1-.34-5.58 2.5 2.5 0 0 1 1.32-4.24 2.5 2.5 0 0 1 4.44-1.5"/><path d="M14.5 2A2.5 2.5 0 0 0 12 4.5v15a2.5 2.5 0 0 0 4.96.44 2.5 2.5 0 0 0 2.96-3.08 3 3 0 0 0 .34-5.58 2.5 2.5 0 0 0-1.32-4.24 2.5 2.5 0 0 0-4.44-1.5"/></svg>`
};
```

### 9.4 CSS 集成代码

```css
.skill-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 28px;
  height: 28px;
  flex-shrink: 0;
  color: var(--accent);
}

.skill-icon svg {
  width: 100%;
  height: 100%;
}
```

### 9.5 渲染逻辑

```javascript
grid.innerHTML = SKILLS.map(s => `
  <div class="skill-card">
    <div class="skill-header">
      <span class="skill-icon">${skillIcons[s.category] || s.icon}</span>
      <h3 class="skill-category">${s.category}</h3>
    </div>
    <div class="skill-items">
      ${s.items.map(item => `<span class="skill-tag">${item}</span>`).join('')}
    </div>
  </div>
`).join('');
```
