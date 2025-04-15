---
title: GitHub Pages + Hexo 搭建静态博客
date: 2025-04-15 13:14
tag: 项目
categories: 前端
---
# 使用 GitHub Pages + Hexo 搭建静态博客

## 目录
1. [准备工作](#1-准备工作)
2. [创建 GitHub 仓库](#2-创建-github-仓库)
3. [安装 Hexo](#3-安装-hexo)
4. [配置 Hexo](#4-配置-hexo)
5. [生成并预览博客](#5-生成并预览博客)
6. [部署到 GitHub Pages](#6-部署到-github-pages)
7. [访问博客](#7-访问博客)
8. [常见问题](#9-常见问题)
10. [后续操作](#10-后续操作)

---

## 1. 准备工作
- **GitHub 账号**：注册一个 [GitHub 账号](https://github.com/)。
- **Node.js 和 npm**：安装 [Node.js](https://nodejs.org/)（自带 npm）。
- **Git**：安装 [Git](https://git-scm.com/)。
- **基础命令行知识**：熟悉终端或命令行工具。

---

## 2. 创建 GitHub 仓库
1. 登录 GitHub，点击右上角 **+** → **New repository**。
2. 仓库名格式：
   - **个人/组织主页**：`<用户名>.github.io`（如 `john.github.io`）。
   - **项目主页**：任意名称（如 `my-blog`），但后续需配置子路径。
3. 设置为 **Public**，然后点击 **Create repository**。

---

## 3. 安装 Hexo
1. **全局安装 Hexo CLI**：
   ```bash
   npm install -g hexo-cli

1. 初始化博客目录 

   ```text
   hexo init my-blog
   cd my-blog
   ```

   - 会生成 `my-blog` 文件夹，包含 Hexo 的配置文件和默认主题。

------

## 4. 配置 Hexo

### 4.1 编辑全局配置文件 `_config.yml`

```yaml
# 站点信息
title: Your Blog Title
subtitle: Your Blog Subtitle
description: Your Blog Description
author: Your Name
language: zh-CN  # 支持中文
timezone: Asia/Shanghai

# 部署配置
deploy:
  type: git
  repo: https://github.com/<用户名>/<仓库名>.git
  branch: main  # 默认分支为 main，旧仓库可能是 master
```



### 4.2 安装主题（以 NexT 为例）

```text
git clone https://github.com/next-theme/hexo-theme-next themes/next
```

- 修改 `_config.yml` 中的 `theme: next`。

------

## 5. 生成并预览博客

1. 生成静态文件 

   ```text
   hexo generate  # 或 hexo g
   ```

2. 本地预览 

   ```text
   hexo server  # 或 hexo s
   ```

   - 访问 `http://localhost:4000` 查看效果。

------

## 6. 部署到 GitHub Pages

1. 安装部署插件 

   ```text
   npm install hexo-deployer-git --save
   ```

2. 部署到 GitHub 

   ```text
   hexo deploy  # 或 hexo d
   ```

   - 首次部署可能需要输入 GitHub 账号密码（建议配置 SSH 密钥）。

------

## 7. 访问博客

- **个人/组织主页** ：访问 `https://<用户名>.github.io`。
- **项目主页** ：访问 `https://<用户名>.github.io/<仓库名>/`。

------

## 8. 常见问题

### 8.1 部署失败

- 检查 `_config.yml` 中的 `repo` 是否正确。
- 确保已安装 `hexo-deployer-git`。

### 8.2 404 错误

- 确认仓库名是否符合规范（个人主页需严格匹配 `<用户名>.github.io`）。
- 检查分支是否为 `main` 或 `master`。

### 8.3 主题不生效

- 确认主题名称是否正确，且已正确安装到 `themes/` 目录。

------

## 9. 后续操作

- **撰写文章** ：`hexo new "文章标题"`，在 `source/_posts` 编辑 Markdown 文件。
- **更新博客** ：修改内容后，运行 `hexo clean && hexo deploy`。
- **自定义主题** ：参考主题文档修改 `themes/<主题名>/_config.yml`。