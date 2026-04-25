---
date: 2026-04-20
authors:
  - liyao
title: Getting Started with MkDocs Material Blog
slug: getting-started-mkdocs-material
description: >
  A quick guide to setting up a programming blog with MkDocs Material — from installation to your first post.
categories:
  - Python
  - Blogging
---

# Getting Started with MkDocs Material Blog

I recently set up this blog to share my programming journey. Here's a quick overview of how it's built.

## Why MkDocs Material?

[MkDocs Material](https://squidfunk.github.io/mkdocs-material/) is a powerful static site generator built on top of MkDocs. It offers:

- **Markdown-first** — write posts in plain Markdown with YAML frontmatter
- **Built-in blog plugin** — categories, authors, archives, and pagination out of the box
- **Beautiful code highlighting** — syntax highlighting with copy buttons
- **Dark mode** — automatic light/dark theme switching
- **Fast search** — full-text search with suggestions

## Project Structure

```
blog/
├── mkdocs.yml          # Site configuration
├── docs/
│   ├── index.md        # Homepage
│   └── posts/          # Blog posts
│       └── *.md        # Each post is a Markdown file
└── venv/               # Python virtual environment
```

## Quick Start

```bash
# Install dependencies
pip install mkdocs-material

# Create a new post
cd docs/posts
cat > my-post.md << 'EOF'
---
date: 2026-04-25
authors:
  - liyao
title: My New Post
categories:
  - General
---

# My New Post

Your content here.
EOF

# Run the dev server
mkdocs serve
```

## What's Next

I plan to write about:

- Python tips and tricks
- Software architecture patterns
- DevOps workflows
- Open source contributions

Stay tuned for more posts!

---

*Happy coding!*
