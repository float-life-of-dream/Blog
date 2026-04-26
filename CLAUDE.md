# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

这是一个使用 MkDocs Material 构建的个人编程博客。博客内容为中文，主题为 Python、软件工程和开发工具。作者使用 float-life-of-dream 作为 GitHub 用户名。

## 常用命令

```bash
# 激活虚拟环境 (Windows PowerShell)
.\venv\Scripts\Activate.ps1

# 启动开发服务器（热重载）
mkdocs serve

# 构建静态站点
mkdocs build --strict

# 安装/更新依赖
pip install -r requirements.txt
```

## 项目结构

```
mkdocs.yml              # 站点配置（主题、插件、导航、社交链接）
docs/
  index.md              # 博客首页
  images/               # Logo (logo.png) 和 favicon (favicon.ico)
  blog/
    .authors.yml        # 作者信息定义
    index.md            # 博客列表页（由 blog 插件自动生成）
    posts/              # 所有博客文章（Markdown 文件）
```

## 博客文章格式

每篇文章是 `docs/blog/posts/` 下的 `.md` 文件，必须包含 YAML frontmatter：

```yaml
---
date: 2026-04-20
authors:
  - liyao
title: 文章标题
slug: article-slug
description: 简短描述
categories:
  - Python
---
```

- `authors` 必须与 `.authors.yml` 中定义的 key 匹配
- `date` 决定文章排序（最新在前）
- `slug` 可选，不指定则从标题自动生成

## 关键配置说明

- `mkdocs.yml` 中 `language: zh` 启用了中文 UI
- `blog_dir: blog` + `post_dir: posts` → 文章路径为 `docs/blog/posts/`
- `.gitignore` 已排除 `site/`，但历史中已跟踪的 `site/` 文件仍会被 git 追踪（构建产物）
- 本地开发使用 Python 虚拟环境 `venv/`

## CI/CD

项目使用 GitHub Actions 自动构建并部署到 GitHub Pages。工作流文件位于 `.github/workflows/ci.yml`，触发条件为 push 到 main/master 分支。