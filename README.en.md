<picture>
  <source media="(prefers-color-scheme: dark)" srcset="readme-assets/header-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="readme-assets/header-light.svg">
  <img alt="SVG Line Icon Workflow · ✦ EricMingle69" src="readme-assets/header-light.svg" width="100%">
</picture>

<p align="center">
  <a href="README.md">简体中文</a> · <a href="README.en.md">English</a> · <a href="PERSONAL-NOTICE.md">✦ EricMingle69</a>
</p>

# SVG Line Icon Workflow

## Purpose

A skill specification and integration examples for consistent web icons, standardizing size, strokes and inherited color for frontend developers, interface designers and AI-agent workflows.

## Repository guide

| Entry | Contents |
| --- | --- |
| [Icon workflow](SKILL.md) | Specification and five-stage workflow |
| [Icon catalog](examples/icon-catalog.md) | Existing categories and path examples |
| [Integration example](examples/resume-icons-demo.html) | HTML inline-icon example |

## Getting started

1. Audit existing icons and read `SKILL.md` to establish categories and integration methods.
2. Validate size, themes and strokes with one representative icon before batch generation and integration checks.
3. Line icons use a `24×24 viewBox`, `stroke-width="2"`, round caps/joins and `currentColor`. Brand icons follow a separate filled style.

## Scope and limitations

- The repository contains specifications and examples, without package configuration, a CLI generator or an installer.
- Check actual readability, theme behavior and accessibility descriptions in the target interface.
- Specific upstream versions, licenses and brand-use rights for SVG paths need item-by-item verification.

## Sources and existing licenses

The original `SKILL.md` references Feather Icons / Lucide for line design and Simple Icons or official logos for brand assets. Preserve third-party and brand attribution. The original repository has no LICENSE/NOTICE and cannot grant a unified license for all icons, paths and logos.

---

Documentation maintained by **✦ EricMingle69** · [Ming-Sir-69](https://github.com/Ming-Sir-69)  
[Personal identity, licensing and permissions](PERSONAL-NOTICE.md) · The header follows your GitHub theme.
