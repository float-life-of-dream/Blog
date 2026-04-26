---
date: 2026-04-20
authors:
  - liyao
title: MkDocs Material 博客搭建指南
slug: getting-started-mkdocs-material
description: >
  从安装到发布第一篇文章，快速搭建一个使用 MkDocs Material 的编程博客。
categories:
  - Python
  - 博客
---

# MkDocs Material 博客搭建指南

最近搭建了这个博客来记录编程旅程。下面简单介绍一下它的构建方式。

## 为什么选 MkDocs Material？

[MkDocs Material](https://squidfunk.github.io/mkdocs-material/) 是一个基于 MkDocs 的强大静态站点生成器。它的优势包括：

- **纯 Markdown** — 使用 Markdown 和 YAML 元数据编写文章
- **内置博客插件** — 开箱即用的分类、作者、归档和分页功能
- **精美的代码高亮** — 带复制按钮的语法高亮
- **深色模式** — 自动切换浅色/深色主题
- **快速搜索** — 带建议的全文搜索

## 项目结构

```
blog/
├── mkdocs.yml          # 站点配置
├── docs/
│   ├── index.md        # 首页
│   └── blog/
│       └── posts/      # 博客文章
│           └── *.md    # 每篇文章是一个 Markdown 文件
└── venv/               # Python 虚拟环境
```

## 快速开始

```bash
# 安装依赖
pip install mkdocs-material

# 创建新文章
cd docs/blog/posts
cat > my-post.md << 'EOF'
---
date: 2026-04-25
authors:
  - liyao
title: 我的新文章
categories:
  - 通用
---

# 我的新文章

在这里写下你的内容。
EOF

# 启动开发服务器
mkdocs serve
```

## 后续计划

我打算写以下主题：

- Python 技巧与窍门
- 软件架构模式
- DevOps 工作流
- 开源贡献

敬请期待更多文章！

---

*Happy coding!*
