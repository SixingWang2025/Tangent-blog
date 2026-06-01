# Tangent Blog

基于 [Hugo](https://gohugo.io/) + [Stack](https://github.com/CaiJimmy/hugo-theme-stack) 主题的个人博客，部署在 [sixingwang2025.github.io/blog/](https://sixingwang2025.github.io/blog/)。

## 目录结构

```
Tangent-blog/
├── config/_default/
│   ├── config.toml      # Hugo 主配置（baseURL, 标题, 分页等）
│   ├── params.toml      # 主题参数（配色、侧栏、文章设置等）
│   ├── menu.toml        # 社交链接与导航菜单
│   ├── markup.toml      # Markdown 渲染配置
│   └── related.toml     # 相关文章配置
├── content/
│   ├── post/            # 文章放在这里（.md）
│   └── page/            # 独立页面放这里
├── assets/
│   └── icons/           # 自定义图标（覆盖主题图标）
├── layouts/             # 自定义模板（覆盖主题模板）
│   └── _partials/
├── static/
│   └── img/             # 静态图片（头像等）
├── themes/
│   └── stack/           # Hugo Stack 主题（git submodule）
└── public/              # 构建输出（提交到仓库用于部署）
```

## 写文章

```bash
# 创建新文章
~/go/bin/hugo new post/文章标题.md

# 本地预览（含草稿）
~/go/bin/hugo server --configDir config --buildDrafts --port 1313
# 访问 http://localhost:1313/blog/
```

文章 front matter 格式：

```yaml
---
title: 文章标题
date: 2026-06-01
description: 文章摘要
tags:
    - 标签1
    - 标签2
categories:
    - 分类
draft: true     # 设为 true 则正式构建时跳过
---
```

## 配置说明

| 文件 | 说明 |
|------|------|
| `config/_default/config.toml` | 站点 URL、语言、标题、分页数量 |
| `config/_default/params.toml` | 侧栏头像、日期格式、小工具、配色方案 |
| `config/_default/menu.toml` | 社交媒体链接（GitHub、RSS 等） |

当前配色设为 `toggle = true, default = "auto"`，支持自动/浅色/深色三种模式。图标已替换为月亮/太阳 SVG（位于 `assets/icons/`）。

## 构建与部署

本仓库采用"本地构建 + 提交 public/"的部署方式：

```bash
# 构建（需要 Hugo extended >= 0.157.0）
~/go/bin/hugo --configDir config

# 提交并推送
git add content/ public/
git commit -m "新文章: xxx"
git push
```

推送到 `main` 后 → GitHub Actions 将 `public/` 部署到 `gh-pages` 分支 → 触发主仓库 `SixingWang2025.github.io` 拉取到 `/blog` 路径。

## Hugo 版本

主题 Stack 要求 Hugo extended ≥ 0.157.0。系统 apt 源版本较旧，推荐用 snap 或 Go 安装：

```bash
# snap 方式
sudo snap install hugo --channel=extended/stable

# Go 方式
GOPROXY=https://goproxy.cn,direct go install -tags extended github.com/gohugoio/hugo@latest
```
