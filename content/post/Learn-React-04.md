---
title: "Learn React 04"
date: 2022-01-29T09:36:59+08:00
draft: false
tags: [React]
categories: [React]
---

> React 使用  create-react-app  创建  react  应用

#### 1、关于  react  脚手架

- react  脚手架是用于帮助程序员快速创建一个基于  react  库的模板项目

  - 包含了所有需要的配置(语法检查、jsx编译、devServer)

  - 下载好了所有相关的依赖
  - 可以直接运行一个简单效果

- react  提供了一个用于创建  react  项目的脚手架库  `create-react-app`

- 项目的整体技术架构为：react  +  webpack  +  es6  + eslint

- 使用脚手架开发的项目的特点：模块化、组件化、工程化

#### 2、创建项目并启动

- 第一步：全局安装  `npm i -g create-react-app`

- 第二步：创建项目  `create-react-app part1`
- 第三步：加入项目文件夹  `cd part1`
- 第四步：启动项目：`npm start`

#### 3、react 脚手架项目结构

```
|- public  静态资源文件夹
  |- favicon.icon  网站页签图标  
  |- index.html    主页面
  |- logo192.png   logo图
  |- logo512.png   logo图
  |- mainfest.json 应用加壳的配置文件
  |- robots.txt    爬虫协议文件
|- src  源码文件夹
  |- App.css      App组件的样式
  |- App.js		  App组件
  |- App.test.js  用于给App做测试
  |- index.css	  样式
  |- index.js	  入口文件
  |- logo.svg  	  logo图
  |- reportWebVitals.js  页面性能分析文件（需要web-vitals库的支持）
  |- setupTests.js		 组件单元测试文件（需要jest-dom库的支持）
```

#### 4、功能界面的组件化编码流程

- 1、拆分组件：拆分界面，抽取组件

- 2、实现静态组件：使用组件实现静态页面效果

- 3、实现动态组件

  - 动态显示初始化数据

    数据类型

    数据名称

    保存在哪个组件？

  - 交互（从绑定事件监听开始）

示例代码：[react_staging](https://github.com/zhishouH/learn-react/tree/main/react_staging)