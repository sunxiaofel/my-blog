---
title: 部署Hexo到GitHub Pages后样式等文件404 Not Found
date: 2024-10-16 12:15:17
tags: 问题记录
banner: /images/deploy-hexo-banner.jpg
excerpt: 是这样的，我本地启动服务是可以正常显示样式等静态资源文件，但是我在部署到 GitHub Pages 之后使用在线链接访问我的博客之后，控制台出现很多条报错，就是静态资源找不到，那么很有就是根路径配置错误原因造成的。
---

## 1. 检查 \_config.yml 中的 url 和 root 配置

Hexo 的配置文件 \_config.yml 中，url 和 root 参数会影响生成的站点中资源文件（如 CSS 和 JS）的路径。如果这些路径设置不正确，可能会导致资源加载失败。

打开项目根目录下的 \_config.yml 文件，检查以下配置：

```yaml
url: http://localhost:4000 # 如果是本地预览
root: / # 如果是部署到根目录
```

如果你部署到一个子目录，配置应当是：

```yaml
url: http://example.com
root: /blog/
```

那么显然我们部署到 GitHub Pages 一定是子目录下，所以使用相对路径。GitHub 中打开项目->Settings->左侧列表找到 Pages 不出意外你会看到 Your site is live at https://username.github.io/my-blog/，这个链接就是作为我们的子目录去打包的

```base
root: https://username.github.io/my-blog/
```

那么这样一番设置后 问题又来了：
我线上可以正常访问了 但是 本地又出问题了。hexo server 后 localhost:4000 页面就无法正常显示 提示报错：Cannot GET ...

# 解决方案

为了解决这个问题，可以使用多环境配置，可以为 Hexo 配置不同的环境变量来分别管理本地开发和生产部署的配置。通过这种方式，在开发环境中设置 root: /，而在生产构建时设置 root: .。

## 在 Hexo 项目的根目录下创建两个配置文件：

config_development.yml
config_production.yml

### 在 config_development.yml 文件中，设置本地开发的 root：

```base
root: /
```

### 在 config_production.yml 文件中，设置构建环境的 root：

```base
root: https://username.github.io/my-blog/
```

### 使用 hexo s 时，指定开发配置文件：

```bash
hexo s --config _config.yml,config_development.yml
```

在构建站点时，使用生产配置文件：

```bash
hexo generate --config _config.yml,config_production.yml
```

这样配置下来，本地和线上都可以正常访问了。
