# SVG 线条图标 · 统一生成与管理

一套面向 Web 界面的 SVG 图标工作流与示例文档。适合需要统一图标笔画、尺寸与颜色继承方式的前端开发者、界面设计者和 AI Agent 使用者。

## 从哪里开始

1. 阅读 [SKILL.md](SKILL.md) 的设计规范与五阶段工作流。
2. 在 [examples/icon-catalog.md](examples/icon-catalog.md) 查找图标目录。
3. 查看 [examples/resume-icons-demo.html](examples/resume-icons-demo.html) 的集成示例，再根据自己的项目选择内联 SVG 或其他集成方式。

核心线条规范为 `24×24 viewBox`、`stroke-width="2"`、圆角端点与连接，以及 `currentColor` 颜色继承。品牌图标在原文中单独使用填充风格处理。工作流从图标审计、规划与一个代表性图标验证开始，再批量生成与集成检查。

## 当前交付范围

仓库包含 Skill 定义和两份示例，没有包管理配置、命令行生成器或一键安装脚本。它提供规范、路径示例和操作约定；图标是否适合目标尺寸、主题及具体项目，需要在集成后检查。

## 来源与许可待确认

原 [SKILL.md](SKILL.md) 明确参考 Feather Icons / Lucide 的线条设计语言，品牌图标参考 Simple Icons 或官方 Logo，并列有相关 SVG 路径。请保留这些来源归属与品牌标识；具体路径的来源版本、许可与商标使用范围仍需逐项核对。

本仓库目前没有 LICENSE 或 NOTICE，不能据此为全部图标、第三方路径和品牌 Logo 提供统一授权。

## 贡献与维护

欢迎通过 Issue 或 Pull Request 改进图标分类、无障碍说明与集成示例。新增路径时请同时提供来源链接、版本和许可证信息，并说明尺寸、线宽与颜色继承方式。

仓库维护：[Ming-Sir-69](https://github.com/Ming-Sir-69)。第三方图标和品牌资源保留各自归属。
