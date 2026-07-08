# 若菡手记

一个关于学习成长、职场心得、旅行生活与运动日常的个人博客。

博客使用 [Hexo](https://hexo.io/) 搭建,采用 [Butterfly](https://butterfly.js.org/) 主题,部署在 [Cloudflare Pages](https://pages.cloudflare.com/)。

---

## 本地开发

### 环境要求

- [Node.js](https://nodejs.org/) >= 18.0
- npm >= 9.0

### 安装依赖

```bash
npm install
```

### 本地预览

```bash
npm run dev
```

访问 `http://localhost:4000` 查看效果。

### 清除缓存

```bash
npm run clean
```

---

## 项目结构

```
Nelumbo/
├── _config.yml                 # Hexo 主配置
├── _config.butterfly.yml       # Butterfly 主题配置 (核心文件)
├── package.json                # 依赖管理
├── .gitignore                  # Git 忽略文件
├── scaffolds/                  # 文章模板
│   ├── post.md
│   ├── page.md
│   └── draft.md
├── source/
│   ├── _posts/                 # 博客文章
│   │   ├── 在职备考软件测试证书的时间规划与高效心得.md
│   │   ├── 软件测试入行三年我踩过的坑和学到的事.md
│   │   ├── 上海出发周末就能去的三个小众宝藏地.md
│   │   └── 坚持夜跑三个月我收获的不只是体重变化.md
│   ├── about/
│   │   └── index.md            # 关于我页面
│   ├── albums/
│   │   └── index.md            # 相册页面
│   ├── categories/
│   │   └── index.md            # 分类页面
│   ├── tags/
│   │   └── index.md            # 标签页面
│   └── img/                    # 图片资源
│       ├── avatar.jpg          # 头像 (待替换)
│       ├── default-cover.jpg   # 默认封面 (待替换)
│       └── albums/             # 相册图片
└── themes/                     # 主题目录 (npm 自动生成)
```

---

## 文章 Front-Matter 规范

每篇文章顶部必须包含以下 front-matter:

```yaml
---
title: 文章标题
date: 2026-07-08 20:00:00          # 发布日期, 格式: YYYY-MM-DD HH:mm:ss
categories:                        # 分类 (只能选一个)
  - 学习成长
tags:                              # 标签 (可以多个)
  - 标签1
  - 标签2
permalink: 2026/07/08/post-slug/   # 永久链接, 格式: YYYY/MM/DD/英文简写/
top_img: false                     # 是否显示顶部封面图
cover: false                       # 是否显示文章封面
---
```

### 分类说明

博客使用以下四个分类:

| 分类 | 说明 | 示例标签 |
|------|------|----------|
| 学习成长 | 学习考证、知识积累 | 软件测试、考证、学习方法 |
| 职场心得 | 工作感悟、职业发展 | 职场成长、新人指南、工作感悟 |
| 旅行生活 | 旅行记录、生活分享 | 旅行、上海周边、小众景点 |
| 运动日常 | 运动记录、健康生活 | 夜跑、运动、生活方式 |

### 发文示例

```yaml
---
title: 周末去了趟莫干山,竹海真的太治愈了
date: 2026-07-15 18:30:00
categories:
  - 旅行生活
tags:
  - 旅行
  - 莫干山
  - 竹海
permalink: 2026/07/15/moganshan-trip/
top_img: false
cover: false
---

正文内容...
```

---

## 部署到 Cloudflare Pages

### 方式一: 通过 Cloudflare Dashboard (推荐)

1. **将代码推送到 GitHub**

```bash
git init
git add .
git commit -m "初始提交: 若菡手记博客"
git remote add origin https://github.com/你的用户名/ruohan-notes.git
git push -u origin main
```

2. **在 Cloudflare Pages 中创建项目**

- 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
- 左侧菜单选择 **Workers & Pages** > **Create** > **Pages**
- 选择 **Connect to Git**
- 授权并选择你的 GitHub 仓库

3. **配置构建设置**

| 配置项 | 值 |
|--------|-----|
| Production branch | `main` |
| Framework preset | `Hexo` |
| Build command | `npm run build` |
| Build output directory | `public` |
| Node.js version | `18` (在 Environment Variables 中设置 `NODE_VERSION=18`) |

4. **添加环境变量**

在项目的 **Settings** > **Environment variables** 中添加:

| 变量名 | 值 |
|--------|-----|
| `NODE_VERSION` | `18` |

5. **保存并部署**

点击 **Save and Deploy**,等待构建完成即可。之后每次推送到 `main` 分支,Cloudflare Pages 会自动重新构建和部署。

### 方式二: 使用 Wrangler CLI

```bash
# 安装 Wrangler
npm install -g wrangler

# 登录 Cloudflare
wrangler login

# 构建
npm run build

# 部署
npx wrangler pages deploy public --project-name=ruohan-notes
```

### 自定义域名

部署完成后,在 Cloudflare Pages 项目设置的 **Custom domains** 中添加你的自定义域名,按照提示配置 DNS 即可。

---

## 图片管理

### 头像替换

将你的个人头像放在 `source/img/avatar.jpg`,建议尺寸 400x400 像素。

### 文章封面

如果需要为文章添加封面图,在 front-matter 中设置:

```yaml
cover: /img/posts/文章名/cover.jpg
```

### 相册图片

相册图片放在 `source/img/albums/` 目录下,在 `source/albums/index.md` 中引用。

---

## 常用命令

```bash
# 新建文章
npx hexo new "文章标题"

# 新建页面
npx hexo new page "页面名称"

# 本地预览
npm run dev

# 构建静态文件
npm run build

# 清除缓存
npm run clean
```

---

## 主题自定义

主题配置文件为 `_config.butterfly.yml`,所有主题相关的样式和功能都在这里修改。

主要配置项:

- **主题色**: `theme_color` 部分
- **导航菜单**: `menu` 部分
- **页脚信息**: `footer` 部分
- **自定义样式**: `inject.head` 部分的 CSS

详细文档参考: [Butterfly 主题文档](https://butterfly.js.org/)

---

## 许可

本站内容采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可协议。

---

> 🌸 记录成长,拥抱生活。
