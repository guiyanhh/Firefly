---
title: 博客网站搭建教程
published: 2026-07-05
date: 2026-07-05 10:00:00
description: 使用firefly搭建网站详细教程
cover: /src/content/posts/images/cover.jpg
tags: [Astro, 静态博客, 部署]
category: 技术教程
draft: false
author: 瑞瑞
---

# 第一篇：前置准备｜安装必备环境

## 一、前言

Firefly 是 Astro 静态博客主题，本文是作者的搭建笔记，为以后回溯搭建过程，为后续操作筑牢基础。

## 二、必备软件清单

- Node.js：核心环境，版本 ≥22

- pnpm

- Git：用于拉取源码、提交代码

- VS Code：推荐编辑器，用于修改配置、写文章

## 三、分步安装教程

### 1、安装 Node.js

1、访问 https://nodejs.org/，下载 LTS 版。

终端执行 node -v、npm -v，输出版本号即成功。

### 2、安装 pnpm

1、终端执行：npm install -g pnpm

2、执行 pnpm -v 输出版本号即成功，权限不足用管理员终端

注意：网络超时切换手机热点。

### 3、安装git

1.访问 https://git-scm.com/download/win，下载最新版并默认安装

2.一直下一步就行了，全程默认安装。

### 4、安装 VS Code（可选）

1.访问 https://code.visualstudio.com/，下载并安装，勾选“创建桌面快捷方式”和“将 Code 加入 PATH”。

![截图](38bf87f316ffbe2b09c0c00737e07000.png)

## 四、常见环境问题排查

node 命令无效 → 重新安装并勾选“Add to PATH”，重启终端/电脑。
pnpm 权限不足 → 用管理员终端执行命令。
git 无反应 → 重启电脑，无效则重装

<br/>

# 第二篇：源码托管｜Fork Firefly 官方仓库

## 一、前言

通过Fork官方仓库，获得自己的独立仓库，可自由修改内容、同步官方更新，后续推送代码到该仓库，Cloudflare会自动触发构建部署。

## 二、前置准备

已完成第一篇环境安装（Node ≥22、pnpm、Git、VS Code）
已注册并登录 GitHub 账号

## 三、Fork 操作步骤（1分钟完成）

1.打开Firefly官方仓库：https://github.com/CuteLeaf/Firefly

2.点击页面右上角的「Fork」按钮（绿色/灰色，位置显眼）。

3.等待3-5秒，页面自动跳转，此时你已拥有「自己的Firefly仓库」（仓库地址：https://github.com/你的GitHub用户名/Firefly）。

关键说明：Fork后的仓库归你所有，修改内容不会影响官方仓库，后续可一键同步官方更新，适合长期维护。

4.配置本地git用户

- git ssh路径

```
C:\Users\Administrator\.ssh
```

- 执行指令

```
# 1. 设置你的GitHub用户名（就是你GitHub主页的用户名）
git config --global user.name "guiyanhh"

# 2. 设置你的GitHub绑定邮箱（就是你注册GitHub用的邮箱）
git config --global user.email "guiyanhh@126.com"
```

- 检测是否成功

```
git config --global user.name
git config --global user.email
```

<br/>

2. 推送到 GitHub：

```
git add .
git commit -m "更新内容"
git push
```

# 第三篇：本地搭建｜克隆仓库 + 本地预览调试

## 一、前言

将你Fork后的仓库克隆到本地，安装依赖后启动本地服务，用于预览修改效果（仅本地查看，无需打包，推送代码后Cloudflare自动部署）。

<br/>

## 二、前置准备

已完成前两篇操作（环境安装、Fork仓库）
新建空文件夹：路径无中文、无空格、无特殊字符（示例：D:\blog）

## 三、克隆你自己的仓库到本地

1.进入 你的 Fork 仓库 页面
2.点击 Code → 复制 HTTPS 地址
3.执行克隆（把地址换成你自己的）： 运行

```
git clone git@github.com:guiyanhh/Firefly.git
```

4.进入项目目录：

```
cd Firefly
```

5.安装本地依赖（仅用于本地预览）

- 安装依赖（用 pnpm） 运行

```
pnpm install
```

- 启动本地预览服务

```
pnpm dev
```

- 等待10-30秒，终端显示访问地址： 
  
  http://localhost:4321

- 打开浏览器输入该地址，看到Firefly默认首页，即本地搭建成功。

- 本地简单调试

修改配置 / 文章 → 保存自动刷新

1.在项目根目录创建wrangler.toml： Cloudflare Workers部署需要

```
name = "firefly"
compatibility_date = "YYYY-MM-DD" # 更为今日

[assets]
directory = "./dist"

[vars]
NODE_VERSION = "22"
```

2.简单修改站点信息。

停止服务：Ctrl + C
重新启动：pnpm dev
本地仅用于预览，无需执行任何打包命令（Cloudflare会自动打包）。

<br/>

- 本地开发完成后

1.先配置本地 Git 身份

打开电脑的终端（Mac/Linux） 或 Git Bash/CMD（Windows），执行 2 条命令：

```
# 1. 设置你的GitHub用户名（就是你GitHub主页的用户名）
git config --global user.name "你的GitHub用户名"

# 2. 设置你的GitHub绑定邮箱（就是你注册GitHub用的邮箱）
git config --global user.email "你的GitHub邮箱"
```

2.检测是否成功

```
git config --global user.name
git config --global user.email
```

3.推送到 GitHub：

```
git add .
git commit -m "更新内容"
git push
```