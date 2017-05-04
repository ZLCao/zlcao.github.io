---
title: Hexo GitHub 分支备份同步
date: 2017-04-29 13:36:27
tags:
  - Hexo
  - GitHub
categories:
  - 技术
  - 博客
---

之前提到 Hexo 博客的源文件是利用 OneDrive 进行同步的。这里说一说用 GitHub 项目分支同步源文件的方法。首先，不妨从新建一个 Hexo 项目开始（{% post_link NexT-Hexo-配置指南 参考这里 %}）。

<!--more-->

按照之前的办法，我们已经可以在本地写博客，利用 OneDrive 同步并发布静态页面到 GitHub 相关项目的 `master` 分支。但项目文件夹里并没有 `.git` 文件夹，要把源文件推送的 GitHub 上，首先要在本地建立一个仓库：
```sh
$ git init .
```
使用 `git clone` 命令安装的主题，自带仓库信息，需要先删除才能正确处理。直接添加文件提交，出错再删除可能导致无法添加这些主题到新建的仓库，通过重命名，或将文件夹移动到别处再移回等方法刷新后再添加提交即可。添加和提交修改命令如下：
```sh
$ git add .
$ git commit -m "commit message"
```
然后，创建一个新的分支：
```sh
$ git checkout -b source
```
并推送到远程仓库：
```sh
$ git remote add origin <repository url>
$ git push -u origin source
```
至此，即完成了一个新建的博客源文件推送到 GitHub 远程仓库的 `source` 分支。

当更换一台新电脑，我们安装好博客环境，直接利用 `git clone` 命令将远程仓库拷贝到本地，并利用 `git checkout` 切换到相应分支，然后安装插件包：
```sh
$ npm install
```
此命令会依据 `package.json` 文件自动安装所有依赖的插件。

由于利用 Hexo 生成的静态页面文件所在文件夹 `public` 是被仓库忽略的，需要利用 `hexo g` 命令重新生成，然后即可利用 `hexo d` 命令发布。