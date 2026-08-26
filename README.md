# minspring-build

[明之小泉](https://minspring.org) 个人博客的构建产物与自动部署仓库。

## 站点

| 站点 | 域名 | 托管 |
| :--- | :--- | :--- |
| 国际站 | <https://minspring.org> | Cloudflare Pages |
| 国内站 | <http://minspring.cn> | 阿里云（蜀ICP备2026010805号） |

## 这个仓库是什么

- 存放 minspring.cn 的**构建产物**（`dist/`，全站静态
  HTML/CSS/JS/图片），以及自动构建部署的 GitHub Actions workflow
- 网站源码（Astro + Notion 作为内容源）保存在私有仓库，不在此公开
- 每日自动从 Notion 拉取最新内容重建：**内容有变化**时提交新
  `dist/` 并部署国内站，同时触发国际站重建；内容无变化则跳过，
  不产生无意义的构建

## 部署方式

GitHub Actions 在海外 runner 构建后，通过 rsync 发布到阿里云服务器
的 `releases/<id>` + `current` 符号链接目录结构（秒级回滚），服务器
只做纯静态 nginx 服务，不跑构建。

## 版权

`dist/` 中的全部文章内容与站点素材版权归 ZHU Quanming 所有。本仓库
公开用于构建透明与内容存档，转载请注明出处并附原文链接。
