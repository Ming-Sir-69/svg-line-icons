# SVG Line Icons — 图标目录速查

> 基于 Feather Icons 设计语言，所有图标遵循统一规范：
> `viewBox="0 0 24 24"` · `fill="none"` · `stroke="currentColor"` · `stroke-width="2"` · `stroke-linecap="round"` · `stroke-linejoin="round"`

## 快速查找

| 语义 | 图标名 | 适用场景 |
|------|--------|---------|
| AI / 机器人 | `bot` | AI Agent、机器学习、自动化 |
| 大脑 / 思维 | `brain` | 方法论、思维模型、认知 |
| 闪电 / 效率 | `zap` | 性能优化、效率提升 |
| 灯泡 / 创意 | `lightbulb` | 想法、创新、灵感 |
| 代码 / 编程 | `code` | 开发、编程语言、技术栈 |
| 终端 / 命令行 | `terminal` | CLI、DevOps、脚本 |
| Git 分支 | `git-branch` | 版本控制、协作开发 |
| 数据库 | `database` | 数据存储、后端 |
| 处理器 | `cpu` | 硬件、性能、计算 |
| 产品 / 模块 | `package` | 产品设计、功能模块 |
| 布局 / 设计 | `layout` | UI 设计、页面结构 |
| 柱状图 | `bar-chart` | 数据可视化、统计 |
| 靶心 / 质量 | `target` | 质量管控、目标管理 |
| 扳手 / 工具 | `tool` | 工程工具、运维 |
| 电话 | `phone` | 联系方式 |
| 邮箱 | `mail` | 邮件联系 |
| 发送 | `send` | 消息发送、提交 |
| 链接 | `link` | URL、引用、关联 |
| 全球 | `globe` | 国际化、网站 |
| 相机 | `camera` | 摄影、截图 |
| 音乐 | `music` | 音频、音乐 |
| 奖项 | `award` | 成就、认证 |
| 星标 | `star` | 收藏、评分、精选 |
| GitHub | `github`（填充） | 代码仓库 |
| LinkedIn | `linkedin`（填充） | 职业社交 |

## 使用方式

### 方式 1：JS 内联对象（推荐）

```javascript
const icons = {
  phone: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>`
};

element.innerHTML = icons.phone;
```

### 方式 2：HTML 直接嵌入

```html
<span class="icon">
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
    <path d="..."/>
  </svg>
</span>
```

### 方式 3：CSS Sprite（大型项目）

```html
<!-- 定义 -->
<svg style="display:none">
  <symbol id="icon-phone" viewBox="0 0 24 24">
    <path d="..."/>
  </symbol>
</svg>

<!-- 使用 -->
<svg class="icon"><use href="#icon-phone"/></svg>
```

## 参考资源

- [Feather Icons](https://feathericons.com/) — 线条图标标准参考
- [Lucide](https://lucide.dev/) — Feather 的社区维护分支，图标更多
- [Simple Icons](https://simpleicons.org/) — 品牌图标权威来源
