---
title: "Hello, 新博客"
description: "新博客的第一篇,介绍技术栈和写博客的目的"
pubDate: 2026-08-06
tags: ["meta", "astro"]
---

这是一个全新的博客,从 Hexo 静态产物仓库重置成了 Astro 5 + Vercel 的组合。

## 为什么换 Astro

之前的博客用的是 Hexo,但因为只保留了 `public/` 产物,没有源码,基本无法维护。换成 Astro 的主要原因:

- **现代化**:基于 Vite,启动和构建都很快
- **TypeScript first**:默认类型安全,减少运行时错误
- **Content Collections**:用 Zod schema 校验 frontmatter,写文章时字段写错会立刻报错
- **零 JS by default**:默认输出纯 HTML,只在需要时再交互,博客天生就适合

## 怎么写新文章

只要在 `src/content/blog/` 下新建一个 `.md` 文件,frontmatter 满足 Zod schema:

```markdown
---
title: "你的文章标题"
description: "一句话描述"
pubDate: 2026-08-06
tags: ["随便打几个标签"]
---

正文写这里。
```

写完 `git push` 到 master,Vercel 会自动重新构建并部署到 `blog.qjq2126.xyz`,大约 1-2 分钟就能看到效果。

## 后续计划

- [ ] 接评论(Giscus / Twikoo 待选)
- [ ] 接入访问统计
- [ ] 写点真正有用的内容