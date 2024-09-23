---
layout: post
title: Deploy RssHub on Vercel(部署 RssHub 在 Vercel 上)
author: AlanZeng
date: 2024-09-17 17:20:30 +0800
tags: Development
---

# Deploy RssHub on Vercel(部署 RssHub 在 Vercel 上)

## 背景

官方推荐使用docker-compose部署RssHub，但是需要个人服务器，而且需要一定的技术水平，而在Vercel上部署RssHub更加简单.

### Vercel 介绍

Vercel 是一个现代化的部署应用程序平台, 有以下优点:
- 部署速度快
- 部署简单
- 支持多种语言

---



## 问题

安装RssHub官方文档进行部署:[https://docs.rsshub.app/deploy/#deploy-to-vercel](https://docs.rsshub.app/deploy/#deploy-to-vercel)

- 部署后会发现下图错误:

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917164759723.png" alt="image-20240917164759723" style="zoom:70%;" />

- 原因是目前[https://github.com/DIYgod/RSSHub](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fgithub.com%2FDIYgod%2FRSSHub&source=article&objectId=2432561)仓库的master分支下, `package.json`设置`"node": ">22"`, 而Vercel平台支持最高为`20.x`

- 解决方案参考[https://github.com/DIYgod/RSSHub/issues/14622](https://github.com/DIYgod/RSSHub/issues/14622)

---



## 部署步骤

### 1. fork原仓库

[https://github.com/DIYgod/RSSHub/fork](https://github.com/DIYgod/RSSHub/fork)

**注意: 在此处取消勾选: Copy the master `branch` only**

<img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917165721730.png" alt="image-20240917165721730" style="zoom:100%;" />

### 2. 部署到vercel

- 访问[https://vercel.com/](https://vercel.com/), 注册账号, 选择Hobby plan

- 进入主页, 点击`Add New... `

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917170024094.png" alt="image-20240917170024094" style="zoom:100%;" />

- 选择`Project`

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917170315369.png" alt="image-20240917170315369" style="zoom:40%;" />

- Import 我们刚刚fork的仓库

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917170457356.png" alt="image-20240917170457356" style="zoom:100%;" />

- 系统会默认生成一个项目名称，也可以自定义修改

- 其他配置不动，点击`Deploy`

- 这里就会遇到开头提到的Error: 当前的环境版本是 `node.js 20`，而`package.json`的要求的 `node.js`版本要`≥22`

- 这里我们的解决方案是使用仓库的`legacy`分支, 该分支设定的`node.js`版本为`≥16`, 满足我们的需求

- 如下图, 进入项目设置, 选择`Git`, 修改`Production Branch`中的`Branch name`为**legacy**, 然后点击`save`保存

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917171024074.png" alt="image-20240917171024074" style="zoom:100%;" />

- 接下来, 在下面的`Deploy Hooks`中创建`legacy on legacy`, 如下图:

  ![image-20240917171239697](https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917171239697.png)

- 访问生成的url, 创建新的deployment, 等待一段时间之后, 就已经部署好了

### 3. 配置域名

- 进入项目设置, 点击`Domains`, 添加域名, 配置DNS解析

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917171630093.png" alt="image-20240917171630093" style="zoom:100%;" />

- 访问配置好的域名, 出现下图, 说明部署完成!

  <img src="https://raw.githubusercontent.com/AlanZeng423/Pics/main/MarkDown_Pics/image-20240917171718131.png" alt="image-20240917171718131" style="zoom:100%;" />

---

## 总结

- 通过Vercel部署RssHub, 可以省去自己搭建服务器的麻烦, 也不用担心服务器的维护问题
- 部署过程中遇到的问题, 通过修改仓库的`legacy`分支, 解决了`node.js`版本不匹配的问题
- 部署完成后, 可以配置域名, 使得访问更加方便
- 通过这次部署, 也学到了如何在Vercel上部署项目, 以及如何配置域名

---

<br>

reference: [https://cloud.tencent.com/developer/article/2432561](https://cloud.tencent.com/developer/article/2432561)
