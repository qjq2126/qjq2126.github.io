# qjq blog

个人博客,基于 **Astro 5** + **Vercel**,部署在 [blog.qjq2126.xyz](https://blog.qjq2126.xyz)。

## 技术栈

- [Astro 5](https://astro.build) — 静态站点生成器
- Content Collections (Astro 5 新 API,基于 glob loader + Zod schema)
- TypeScript strict mode
- 极简自写主题(无 Tailwind)
- Vercel 自动部署,域名 blog.qjq2126.xyz
- Let's Encrypt SSL 自动续期

## 目录结构

```
.
├── astro.config.mjs        # Astro 配置
├── src/
│   ├── content.config.ts   # Content Collections schema (Zod)
│   ├── content/
│   │   └── blog/           # Markdown 文章
│   ├── layouts/
│   │   └── Layout.astro    # 站点布局
│   ├── pages/
│   │   ├── index.astro     # 首页
│   │   ├── archives.astro  # 归档页
│   │   ├── about.astro     # 关于页
│   │   ├── blog/[...slug].astro  # 文章详情路由
│   │   └── rss.xml.ts      # RSS 订阅
│   └── styles/
│       └── global.css      # 全站样式(含暗色模式)
└── public/
    ├── favicon.svg
    └── robots.txt
```

## 怎么写新文章

在 `src/content/blog/` 下新建一个 Markdown 文件,frontmatter 遵循 `src/content.config.ts` 里的 Zod schema:

```markdown
---
title: "你的标题"
description: "一句话描述"
pubDate: 2026-08-06
tags: ["技术", "生活"]
draft: false
---

正文
```

可选字段:`updatedDate`(更新时间)、`draft`(是否草稿,draft 文章不会出现在列表和 RSS 里)。

## 本地开发

环境要求:Node.js >= 18。

```bash
# 走代理(国内网络建议)
HTTPS_PROXY=http://127.0.0.1:7890 HTTP_PROXY=http://127.0.0.1:7890 npm install

# 启动开发服务(http://localhost:4321)
npm run dev

# 构建生产产物到 dist/
npm run build

# 本地预览生产产物
npm run preview
```

## 部署

```bash
git add .
git commit -m "your message"
HTTPS_PROXY=http://127.0.0.1:7890 git push origin master
```

Vercel 会监听 push,自动 `npm install` + `npm run build`,然后部署到 `blog.qjq2126.xyz`。通常 1-2 分钟生效。

## 暗色模式

样式表里用 `prefers-color-scheme: dark` 自动跟随系统设置。如果想加手动切换,可以扩展 `Layout.astro` 加一段 JS。

## 路线图(暂定)

- [ ] 接评论系统(Giscus 或 Twikoo)
- [ ] 接入访问统计(可能用 Plausible 自部署)
- [ ] 标签页 + 搜索
- [ ] 文章目录(TOC)