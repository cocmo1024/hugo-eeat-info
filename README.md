# 🧠 hugo-eeat-info

> Hugo 模块：增强页面可信度，助力 Google EEAT（专业性、权威性、可信度）评分

本模块旨在为博客或内容网站添加结构化的作者信息、相关文章推荐等内容块，以增强 Google 对页面内容的信任和评分。

---

## 📦 模块包含内容

| 模板名 | 功能说明 |
|--------|----------|
| `partials/eeat/author-box.html` | 显示作者信息（姓名、头像、描述） |
| `partials/eeat/related-posts.html` | 展示相关文章推荐列表 |
| `partials/eeat/eeat-footer.html` | 统一调用作者信息与相关文章的页脚模块 |
| `partials/eeat/update-meta.html` | 可用于后期拓展如“最近更新”提示等功能（当前为保留模板） |

---

## 🛠️ 使用方法

### 1. 模块引入（站点 `config.yaml` 中）

```yaml
module:
  imports:
    - path: github.com/yourusername/hugo-eeat-info
      mounts:
        - source: layouts
          target: layouts
````

> 🔁 请将 `yourusername` 替换为你的 GitHub 用户名或模块路径。

---

### 2. 页面调用（在文章模板或主题中调用）

推荐在 `layouts/_default/single.html` 中添加：

```go-html-template
{{ partial "eeat/eeat-footer.html" . }}
```

也可单独调用作者信息或相关文章模块：

```go-html-template
{{ partial "eeat/author-box.html" . }}
{{ partial "eeat/related-posts.html" . }}
```

---

## 🧑‍💼 作者信息配置方式

在 `config.yaml` 或每篇文章 front matter 中添加以下参数：

### 全局配置（站点级 `params`）

```yaml
params:
  author: "Walter"
  authorAvatar: "/images/avatar.webp"
  authorBio: "内容创作者、自动化系统设计者，专注于 AI 与低代码应用"
```

### 页面级覆盖（文章 front matter）

```yaml
---
title: "如何构建可盈利的内容站群"
author: "Walter"
authorAvatar: "/images/avatar-special.png"
authorBio: "资深 SEO 策略师，10 年内容营销经验"
---
```

---

## 🔗 相关文章推荐设置

系统将调用 `.Site.RegularPages.Related . | first 5`，相关性依赖以下站点配置：

```yaml
related:
  threshold: 80
  includeNewer: true
  toLower: true
  indices:
    - name: keywords
      weight: 100
    - name: tags
      weight: 80
    - name: categories
      weight: 60
    - name: date
      weight: 10
```

确保每篇文章有 tags、keywords 或 categories 字段。

---

## 📁 文件结构

```
hugo-eeat-info/
├── layouts/
│   └── partials/
│       └── eeat/
│           ├── author-box.html
│           ├── related-posts.html
│           ├── eeat-footer.html
│           └── update-meta.html
├── go.mod
└── README.md
```

---

## 🧪 兼容性

✅ 与 PaperMod、LoveIt 等 Hugo 主流主题兼容
✅ 模块高度解耦，不影响主题原有功能
✅ 完全可复用，适用于站群系统

---

