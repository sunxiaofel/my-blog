---
title: Hexo配置网站图标
date: 2024-10-16 11:22:12
tags: 问题记录
---

不知道是不是Hexo不支持ico后缀文件作为网站的图标，新创建的项目打开F12就会看到一个报错：GET http://localhost:4000/favicon.png 404 (Not Found)，注意看后缀名不是ico，而是png，然后 我在_config.yml文件中企图使用自定义配置来更改它，但是也无济于事。所以这篇文章中也是使用了png文件作为的网站图标，个人觉得不妥，但搜集资料后无果，暂时先用这种方法解决吧！

# 情景重现（无法解决）

## 1.放置 favicon.ico 文件
将生成的favicon.ico文件放置在Hexo项目的 source 文件夹下。路径如下：
```bash
/source/favicon.ico
```

## 2.配置_config.yml
如果你的Hexo主题有自己的配置文件（通常是_config.yml），找到用于配置 favicon 的字段，并将其指向你的 favicon.ico 文件。例如，某些主题的配置可能如下：

```yaml
favicon: /favicon.ico
```

## 3.清除缓存并重新生成网站
执行以下命令，清除Hexo缓存并重新生成站点：
```bash
hexo clean
hexo build
```

## 4.运行本地服务器
```bash
hexo s
```
清除浏览器缓存并重新加载后你会发现图标依旧不显示，并且F12打开控制台依旧报错找不到favicon.png文件

# 解决方法
这种情况我个人认为是Hexo支持的网站图标可能就是png文件但又同其他框架来说显得不符合常理，一个网站图标而已 只要显示出来就行了（嘿嘿），所以接下来的方法就是 只需要将你的图标文件改为后缀名为png格式，再将它放置source目录中即可，然后执行第三步、第四步你就会看到你的网站图标成功显示！