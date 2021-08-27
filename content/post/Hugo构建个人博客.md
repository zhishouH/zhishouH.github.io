---
title: "Hugo构建个人博客"
date: 2021-08-27T11:26:47+08:00
draft: false
---

> Hugo构建个人博客

## 安装Hugo

#### 二进制安装(简单、快速)

到[ Hugo Releases](https://github.com/gohugoio/hugo/releases)下载对应的操作系统版本的Hugo二进制文件(hugo或hugo.exe)



## 生成站点

使用Hugo快速生成站点，比如希望生成到**/e/Desktop/site**路径：

`$hugo new site /e/Desktop/site`

这样就在**/e/Desdktop/site**目录里生成了初始站点，进去目录：

`cd /e/Desktop/site`

站点目录：

```apl
|- archetypes
|- content
|- data
|- layouts
|- static
|- themes
|- config.toml
```



## 创建文章

创建一个**about**页面：

`$ hugo new about/index.md`

**index.md**生成到了**content/about/index.md**



## 安装皮肤

技术型博客主题[maupassant-hugo](https://github.com/flysnow-org/maupassant-hugo)

`git clone https://github.com/flysnow-org/maupassant-hugo themes/maupassant`



## 运行Hugo

在站点根目录执行`hugo server`命令进行调试

浏览器里打开 ` http://localhost:1313/`





