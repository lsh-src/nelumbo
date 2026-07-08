# 若菡手记 — 部署指南

## 📋 目录

- [部署平台选择](#部署平台选择)
- [Cloudflare Pages 部署](#cloudflare-pages-部署)
- [Vercel 部署](#vercel-部署)
- [GitHub Pages 部署](#github-pages-部署)
- [域名配置](#域名配置)
- [SEO 优化](#seo-优化)

---

## 部署平台选择

| 平台 | 免费额度 | 自定义域名 | 国内访问 | 推荐度 |
|------|----------|------------|----------|--------|
| **Cloudflare Pages** | ✅ 无限 | ✅ 支持 | ⚡ 快 | ⭐⭐⭐⭐⭐ |
| **Vercel** | ✅ 100GB/月 | ✅ 支持 | 🚀 较快 | ⭐⭐⭐⭐ |
| **GitHub Pages** | ✅ 无限 | ✅ 支持 | 🐢 慢 | ⭐⭐⭐ |
| **Netlify** | ✅ 100GB/月 | ✅ 支持 | 🚀 较快 | ⭐⭐⭐⭐ |

**推荐**：**Cloudflare Pages** — 免费、速度快、支持自定义域名、自带 CDN。

---

## Cloudflare Pages 部署

### 步骤 1：准备 Git 仓库

```bash
# 初始化 Git 仓库
git init
git add .
git commit -m "Initial commit"

# 推送到 GitHub
git remote add origin https://github.com/你的用户名/ruohan-notes.git
git push -u origin main
```

### 步骤 2：登录 Cloudflare

1. 访问 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 注册/登录账号
3. 左侧菜单选择 **Pages**

### 步骤 3：创建项目

1. 点击 **Create a project**
2. 选择 **Connect to Git**
3. 授权 GitHub 并选择仓库
4. 配置构建设置：
   - **Production branch**: `main`
   - **Build command**: `npm run build`
   - **Build output directory**: `public`
5. 点击 **Save and Deploy**

### 步骤 4：等待部署

部署完成后，你会得到一个免费域名：`ruohan-notes.pages.dev`

---

## Vercel 部署

### 步骤 1：安装 Vercel CLI

```bash
npm install -g vercel
```

### 步骤 2：登录并部署

```bash
# 登录
vercel login

# 部署
vercel

# 生产环境部署
vercel --prod
```

### 步骤 3：配置

Vercel 会自动检测 Hexo 项目，无需额外配置。

部署完成后，你会得到一个免费域名：`ruohan-notes.vercel.app`

---

## GitHub Pages 部署

### 步骤 1：创建 GitHub Actions

创建文件 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install Dependencies
        run: npm install

      - name: Build
        run: npm run build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

### 步骤 2：配置仓库

1. 进入仓库 Settings → Pages
2. Source 选择 **GitHub Actions**
3. 推送代码后自动部署

部署完成后，你会得到一个免费域名：`你的用户名.github.io/ruohan-notes`

---

## 域名配置

### 购买域名

推荐域名注册商：
- [Namesilo](https://www.namesilo.com/) — 便宜、免费隐私保护
- [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/) — 成本价、无溢价
- [Namecheap](https://www.namecheap.com/) — 经常有优惠

### 绑定自定义域名

#### Cloudflare Pages

1. 进入项目 → **Custom domains**
2. 添加域名（如 `ruohan-notes.com`）
3. 按提示添加 DNS 记录：
   ```
   类型: CNAME
   名称: @ 或 www
   目标: ruohan-notes.pages.dev
   ```

#### Vercel

1. 进入项目 → **Settings → Domains**
2. 添加域名
3. 按提示添加 DNS 记录

### DNS 配置示例

```
# 主域名
ruohan-notes.com      → CNAME → ruohan-notes.pages.dev

# www 子域名
www.ruohan-notes.com  → CNAME → ruohan-notes.pages.dev
```

---

## SEO 优化

### 1. 更新网站配置

编辑 `_config.yml`：

```yaml
# 更新为实际域名
url: https://ruohan-notes.com
```

### 2. 提交搜索引擎

- **Google**: [Google Search Console](https://search.google.com/search-console)
- **Bing**: [Bing Webmaster Tools](https://www.bing.com/webmasters)
- **百度**: [百度搜索资源平台](https://ziyuan.baidu.com/)

### 3. 生成 Sitemap

安装插件：
```bash
npm install hexo-generator-sitemap --save
```

在 `_config.yml` 添加：
```yaml
sitemap:
  path: sitemap.xml
```

### 4. robots.txt

创建 `source/robots.txt`：

```
User-agent: *
Allow: /
Sitemap: https://ruohan-notes.com/sitemap.xml
```

---

## 快速部署命令

```bash
# 构建
npm run build

# 本地预览
npm run server

# 部署到 Cloudflare Pages (推荐)
# 只需要推送到 GitHub，Cloudflare 会自动部署
git add .
git commit -m "Update content"
git push origin main
```

---

## 常见问题

### Q: 部署后图片不显示？

A: 检查图片路径是否正确，确保图片在 `source/img/` 目录下。

### Q: 如何更新网站？

A: 只需要推送代码到 GitHub，Cloudflare Pages 会自动重新部署。

### Q: 如何查看访问统计？

A: 推荐使用 [Umami](https://umami.is/) — 免费、隐私友好的访问统计。

### Q: 国内访问慢怎么办？

A: 使用 Cloudflare Pages 自带 CDN，或者考虑使用国内 CDN（如腾讯云 CDN）。

---

## 推荐域名

根据你的博客主题，推荐以下域名：

- `ruohan-notes.com` — 简洁明了
- `ruohan.life` — 生活记录
- `ruohan.blog` — 博客专用
- `ruohan.site` — 通用

---

**祝部署顺利！** 🚀

如果遇到问题，可以参考：
- [Cloudflare Pages 文档](https://developers.cloudflare.com/pages/)
- [Vercel 文档](https://vercel.com/docs)
- [Hexo 部署文档](https://hexo.io/zh-cn/docs/deployment)
