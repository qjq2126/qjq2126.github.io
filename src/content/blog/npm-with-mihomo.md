---
title: "在 Ubuntu 上用 mihomo 代理给 npm 加速"
description: "记录一下本机 npm install 走 mihomo 代理的方法,以及 Vercel 端为什么不需要"
pubDate: 2026-08-06
tags: ["技术", "工具", "代理"]
---

本机环境是 Ubuntu Server,装了 [mihomo](https://github.com/MetaCubeX/mihomo)(原 Clash Meta)做代理,监听 `127.0.0.1:7890`。在这个环境下给 Node 项目装依赖,直接 `npm install` 经常慢或超时。

## 最简单的办法:走环境变量

```bash
HTTPS_PROXY=http://127.0.0.1:7890 HTTP_PROXY=http://127.0.0.1:7890 npm install
```

或者临时写进 shell:

```bash
export HTTPS_PROXY=http://127.0.0.1:7890
export HTTP_PROXY=http://127.0.0.1:7890
export http_proxy=$HTTP_PROXY
export https_proxy=$HTTPS_PROXY
npm install
```

`git push` 也需要,因为 GitHub 在国内连通性差。

## 长期生效:写到 npm 配置

```bash
npm config set proxy http://127.0.0.1:7890
npm config set https-proxy http://127.0.0.1:7890
```

要恢复:

```bash
npm config delete proxy
npm config delete https-proxy
```

## Vercel 端为什么不用

Vercel 在海外构建机房里构建,直连 GitHub 和 npm registry 都没问题。本机代理只解决"我自己机器到外网"这一段,服务器在云端不需要。

## 常见坑

- 走代理后某些脚本下载会变慢(因为多了代理一跳),但总体比直连稳定
- `git push` 走代理前先确认 `git config --global http.proxy` 没设错
- `curl` 命令别忘了也带 `HTTPS_PROXY`,否则会一直连不上