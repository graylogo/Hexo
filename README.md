# Gray's Blog

一个基于 Hexo + Fluid 主题的技术博客，主要用于记录技术笔记和思考。

## 技术栈

- **框架**：Hexo 8.1.1
- **主题**：Fluid
- **部署**：GitHub Pages
- **域名**：grayblog.cn

## 目录结构

```
├── _config.yml          # Hexo 核心配置文件
├── _config.fluid.yml    # Fluid 主题配置文件
├── source/              # 源文件目录
│   ├── _posts/          # 文章目录
│   ├── CNAME            # 域名配置文件
│   └── ...
├── public/              # 生成的静态文件
├── themes/              # 主题目录
├── package.json         # 依赖配置
└── README.md            # 项目说明
```

## 快速开始

### 1. 安装依赖

```bash
npm install
```

### 2. 本地预览

```bash
hexo s
```

访问 http://localhost:4001 查看博客

### 3. 生成静态文件

```bash
hexo g
```

### 4. 清理缓存

```bash
hexo clean
```

### 5. 生成并部署

```bash
hexo g -d
```

## 写作指南

### 创建新文章

```bash
hexo new "文章标题"
```

### 文章 Front-matter

```yaml
title: 文章标题
date: 2026-01-19 10:00:00
categories: 分类名称
tags: [标签1, 标签2]
---
```

### 文章内容格式

- 使用 Markdown 语法
- 支持代码高亮
- 支持图片插入
- 支持数学公式

## 配置说明

### 核心配置文件

1. **_config.yml**：Hexo 核心配置
   - 网站基本信息
   - URL 配置
   - 主题配置
   - 部署配置

2. **_config.fluid.yml**：Fluid 主题配置
   - 主题样式
   - 导航菜单
   - 首页配置
   - 文章页配置
   - 代码高亮
   - 搜索功能

### 重要配置项

#### Hexo 配置

```yaml
# 网站基本信息
title: Gray's Blog
author: Gray
language: zh-CN

# URL 配置
url: https://grayblog.cn

# 主题配置
theme: fluid

# 部署配置
deploy:
  type: git
  repo: git@github.com:graylogo/gray.github.io.git
  branch: master
```

## 部署说明

### 部署到 GitHub Pages

1. **配置 GitHub 仓库**
   - 创建名为 `graylogo.github.io` 的仓库
   - 配置 CNAME 文件指向域名 `grayblog.cn`

2. **配置 SSH 密钥**
   - 生成 SSH 密钥：`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
   - 把公钥添加到 GitHub

3. **部署命令**
   ```bash
   hexo g -d
   ```

### 部署结果

- 博客地址：https://grayblog.cn
- 仓库地址：https://github.com/graylogo/gray.github.io

## 主题特色

- ✅ 现代化响应式设计
- ✅ 支持暗色模式
- ✅ 内置搜索功能
- ✅ 代码高亮
- ✅ 数学公式支持
- ✅ 阅读时长统计
- ✅ 字数统计
- ✅ 文章卡片设计

## 注意事项

1. **域名配置**
   - 确保 CNAME 文件存在且内容为 `grayblog.cn`
   - 确保 DNS 解析正确

2. **主题配置**
   - 修改主题配置后需要重新生成并部署
   - 配置文件对缩进敏感，建议使用空格缩进

3. **依赖管理**
   - 定期更新依赖：`npm update`
   - 注意依赖版本兼容性

4. **备份**
   - 定期备份源文件和配置文件
   - GitHub 仓库会自动备份

## 常见问题

### Q: 本地预览正常，部署后样式错乱？
A: 检查 URL 配置是否正确，确保使用 HTTPS。

### Q: 文章无法搜索到？
A: 确保搜索功能已开启，重新生成搜索索引。

### Q: 部署后域名无法访问？
A: 检查 CNAME 配置和 DNS 解析，等待 DNS 生效。

## 更新日志

- 2026-01-19: 升级到 Hexo 8.1.1，更换为 Fluid 主题
- 2026-01-19: 优化主题配置，添加 README 文档

## 许可证

MIT

## 联系方式

- 博客：https://grayblog.cn
- GitHub：https://github.com/graylogo
