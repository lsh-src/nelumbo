# 图片资源目录

此目录用于存放博客中使用的图片资源。

## 目录结构建议

```
img/
├── avatar.jpg          # 个人头像 (建议 400x400 像素, 圆形裁剪友好)
├── default-cover.jpg   # 文章默认封面图 (建议 1200x800 像素)
├── albums/             # 相册图片
│   ├── travel-cover.jpg
│   ├── shanghai-cover.jpg
│   ├── daily-cover.jpg
│   └── kaifeng-cover.jpg
└── posts/              # 文章内嵌图片
    ├── post-01/
    ├── post-02/
    └── ...
```

## 图片使用方式

在 Markdown 文章中引用图片:

```markdown
![图片描述](/img/posts/post-01/photo.jpg)
```

## 图片优化建议

- 文章封面图: 1200x800 像素, JPG 格式, 质量 80%
- 文章内嵌图: 宽度不超过 1200 像素
- 头像: 400x400 像素, JPG 或 PNG 格式
- 相册封面: 800x600 像素, JPG 格式
- 使用 [TinyPNG](https://tinypng.com/) 压缩图片后再上传
