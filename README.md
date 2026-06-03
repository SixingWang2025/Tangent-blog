# Tangent Blog

基于 [Hugo](https://gohugo.io/) + [Stack](https://github.com/CaiJimmy/hugo-theme-stack) 主题的个人博客，上线地址：[**sixingwang2025.github.io/blog/**](https://sixingwang2025.github.io/blog/) 。

## 目录结构

```
Tangent-blog/
├── config/_default/
│   ├── config.toml      # Hugo 主配置（baseURL、标题、分页等）
│   ├── params.toml      # 主题参数（侧栏、配色、文章设置）
│   ├── menu.toml        # 社交链接与导航菜单
│   ├── markup.toml      # Markdown 渲染配置
│   └── related.toml     # 相关文章推荐配置
├── content/
│   ├── post/            # ★ 文章放这里（.md）
│   └── page/            # 独立页面放这里
├── assets/
│   └── icons/           # 自定义图标（覆盖主题默认图标）
├── layouts/             # 自定义模板（覆盖主题模板）
├── static/
│   └── img/             # 静态图片（头像、文章插图等）
├── themes/
│   └── stack/           # Hugo Stack 主题（git submodule）
└── public/              # Hugo 构建输出（提交到仓库，用于部署）
```

## 写文章

```bash
# 创建新文章
hugo new post/文章标题.md

# 本地预览（含草稿）
hugo server --configDir config --buildDrafts --port 1313
# 访问 http://localhost:1313/blog/
```

文章 front matter：

```yaml
---
title: 文章标题
date: 2026-06-01
description: 文章摘要
tags:
    - 标签1
    - 标签2
categories:
    - 分类名
draft: true     # 草稿=true 则构建时跳过；发布前改为 false
---
```

## 配置说明

| 文件 | 用途 |
|------|------|
| `config/_default/config.toml` | 站点 URL、语言（zh-cn）、标题、分页（5篇/页） |
| `config/_default/params.toml` | 侧栏头像、日期格式、文章目录、Widget、配色 |
| `config/_default/menu.toml` | 社交媒体图标：导航站 / 个人主页 / GitHub / RSS |

### 配色

支持自动 / 浅色 / 深色三种模式，默认跟随系统：

```toml
[color]
    toggle = true
    default = "auto"
```

亮/暗模式图标已覆盖为月亮/太阳 SVG，位于 `assets/icons/`。

## 构建与部署

采用"本地构建 + 提交 public/"的方式：

```bash
# 构建（需要 Hugo extended）
hugo --configDir config

# 提交并推送
git add content/ public/
git commit -m "新文章: xxx"
git push
```

推送 `main` → GitHub Actions 将 `public/` 部署到 `gh-pages` 分支 → 主仓库 `SixingWang2025.github.io` 拉取到 `/blog/` 路径。

## 环境要求

- **Hugo extended** ≥ 0.157.0（Stack 主题要求）
- 系统 apt 源版本较旧，推荐 snap 或 Go 安装：

```bash
# snap（推荐）
sudo snap install hugo --channel=extended/stable

# Go 安装
GOPROXY=https://goproxy.cn,direct go install -tags extended github.com/gohugoio/hugo@latest
```
