# gaothink-assets

Public assets (images, thumbnails, diagrams) for [gaothink.in](https://github.com/Gao-thinking/gaothink.in).

Served via [jsDelivr CDN](https://www.jsdelivr.com/) with global acceleration.

## URL Format

```
https://cdn.jsdelivr.net/gh/Gao-thinking/gaothink-assets@main/{type}/{slug}/{filename}
```

| type | 对应内容 |
|---|---|
| `blog` | 博客文章（zh/en 共享同一图片目录） |
| `weekly` | 周刊 |
| `lab` | 实验室项目 |
| `product` | 作品集 |
| `site` | 站点级资源（favicon、og-image 等） |

## Directory Structure

```
gaothink-assets/
├── blog/
│   ├── content-workflow/          # slug 做目录名（去掉日期前缀）
│   │   ├── cover.png
│   │   ├── architecture.png
│   │   └── deploy-flow.png
│   ├── another-post/
│   │   └── ...
│   └── _shared/                   # 跨文章复用的资源（logo、图标）
│       └── logo.png
├── weekly/
│   └── issue-001/
│       └── thumbnail.png
├── lab/
│   └── desk-organizer/
│       └── hero.jpg
├── product/
│   └── memo-genius/
│       └── hero.png
├── site/
│   ├── og-default.png
│   └── favicon.ico
└── README.md
```

## Naming Conventions

### 目录命名

- **目录名 = 内容 slug**：`blog/content-workflow/` ↔ `content/blog/zh/2026-06-18-content-workflow.mdx`
- 去掉日期前缀，用 slug 做目录名
- zh/en 共享同一图片目录（图片不翻译，URL 一致）

### 文件命名

| 命名 | 含义 |
|---|---|
| `cover.png` / `hero.jpg` | 封面/主图 |
| `architecture.png` | 架构图 |
| `screenshot-*.png` | 截图，带说明 |
| `diagram-*.png` | 示意图 |
| `before.png` / `after.png` | 对比图 |

**禁止**：`image1.png`、`IMG_20260618.png`、`截图.png`、`未命名.png`

### 支持的格式

`.png` `.jpg` `.jpeg` `.gif` `.webp` `.svg`

单文件大小限制 25MB（GitHub web 上传限制）。超过的视频走 YouTube/B 站外链。

## Upload Workflow

### 自动上传（推荐）

在 gaothink.in private repo 里写完文章后：

```bash
pnpm assets:upload
```

脚本会自动：
1. 扫描 `content/` 下所有 `.assets/` 目录
2. 复制图片到本 repo 的 `{type}/{slug}/` 目录
3. git push 到本 repo
4. 替换 MDX 里的相对路径为 jsDelivr CDN URL
5. 移动本地原图到 `/tmp/gaothink-assets-moved/` 归档

### 手动上传

直接 clone 本 repo，按目录结构放图片，push 即可。

```bash
git clone git@github.com:Gao-thinking/gaothink-assets.git
# 放图片到 blog/your-slug/
git add .
git commit -m "add: images for your-slug"
git push
```

## CDN Cache

jsDelivr 缓存 12 小时。更新图片后想立刻生效：

1. 改文件名：`foo.png` → `foo-v2.png`
2. 或用 commit hash 锁定：`@main` → `@abc1234`

## Related

- 主项目：[gaothink.in](https://github.com/Gao-thinking/gaothink.in)（private）
- 写作规范：[.claude/project-context.md](https://github.com/Gao-thinking/gaothink.in/blob/main/.claude/project-context.md)
