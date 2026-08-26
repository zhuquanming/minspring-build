# minspring-build

minspring.cn 的构建与部署管线仓库(PUBLIC)。

## 为什么存在

私有仓库 `astro-notion-blog` 的 GitHub Actions 免费额度(2000 Linux
分钟/月)已耗尽,deploy 任务被 billing 拦截。**Public 仓库的 Actions
免费不限量**,因此把"构建+部署"这一重活搬到本仓库执行,源码继续
留在 private 仓库。

## 工作方式

1. Workflow `deploy.yml`(每日 04:22 北京时间 + 手动触发)用
   `SOURCE_REPO_TOKEN` checkout private 源码仓库
2. 以 `SITE_VARIANT=cn CUSTOM_DOMAIN=minspring.cn` 构建
3. 构建产物 `dist/` 提交回本仓库——"构建内容放 public,代码留
   private"
4. rsync 到阿里云服务器,原子切换 `current` 符号链接

## Secrets

| 名称 | 用途 |
| :--- | :--- |
| SOURCE_REPO_TOKEN | 拉取 private 源码仓库(git checkout) |
| NOTION_API_SECRET | Notion API 集成 token(构建数据源) |
| DATABASE_ID | Notion 数据库 ID |
| CHINA_DEPLOY_KEY | 阿里云部署 SSH 私钥(仅限 rsync 目标目录) |

Fork PR 无法读取 secrets(GitHub 默认安全行为)。

## 相关

- 源码:zhuquanming/astro-notion-blog(private)
- 线上:<http://minspring.cn(阿里云,纯静态> nginx)
- 国际站:<https://minspring.org(Cloudflare> Pages)
