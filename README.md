# FastDeployTemplate

<p align="center">
  <img src="./logo.png" alt="FastDeploy Logo" width="120" height="120" />
</p>

A streamlined GitHub Actions template powered by **Quartz v5**, designed to accelerate your journey from drafting Markdown notes to deploying a modern digital garden on GitHub Pages.

---

## 特性 (Features)

- 🚀 **开箱即用**：无需手动安装复杂环境，基于 GitHub Actions 全自动构建并部署至 GitHub Pages。
- ⚙️ **Quartz v5 驱动**：支持双向链接、交互式图谱（Graph View）、全文检索与 Obsidian Markdown 语法。
- 📂 **根目录作为内容源**：直接在仓库中编写 Markdown 笔记，无需多层嵌套。
- 🎨 **高度可定制**：通过根目录下的 `quartz.config.yaml` 自定义站点名称与链接，通过 `custom.scss` 定制主题样式。
- 🖼️ **品牌资产支持**：站点图标与 Header Logo 支持根目录的 `logo.svg`（优先）或 `logo.png`，构建时自动生成 favicon。

---

## 配置文件说明 (Configuration)

- [`quartz.config.yaml`](./quartz.config.yaml)：**完整**站点配置（名称、语言、Base URL、主题与插件）。
  > ⚠️ Quartz v5 会用该文件整体替换引擎自带的默认配置，不会做合并。请勿删除 `configuration.theme`、`configuration.ignorePatterns`，以及 `content-page` / `folder-page` / `tag-page` 等核心插件，否则构建会报错或只生成 404 页面。
- [`custom.scss`](./custom.scss)：自定义样式（包括页面标题 Logo 注入）。
- [`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml)：GitHub Actions 自动化构建部署流。
- `logo.svg` / [`logo.png`](./logo.png)：站点 Logo（二选一，SVG 优先），同时用于 Header 与 Favicon。

### Logo

根目录放置 `logo.svg` **或** `logo.png` 即可（站点构建二选一），两者同时存在时优先使用 SVG：

- Header Logo 直接引用源文件（通过 CSS 变量 `--logo-image`）；
- 使用 SVG 时，构建会用引擎自带的 `sharp` 生成 512×512 的 `logo.png`（供 README 展示）和 128×128 的 `static/icon.png`（供 favicon），无需手动转换；
- 使用 PNG 时按原样复制为 favicon 源。

> 仓库 README 顶部图片引用的是 `logo.png`。如果只提交 SVG，请同时保留一张 PNG，或把 README 里的 `./logo.png` 改成 `./logo.svg`。

## 常见问题 (Troubleshooting)

### `Cannot read properties of undefined (reading 'fontOrigin')`

`quartz.config.yaml` 缺少 `configuration.theme` 块。v5 的 YAML 配置是整体替换而非与默认值合并，因此 `theme`（含 `fontOrigin`、`cdnCaching`、`typography`、`colors`）必须显式书写。补齐后若出现 `cfg.configuration.ignorePatterns is not iterable`，同理补上 `ignorePatterns: []` 或具体排除项。

