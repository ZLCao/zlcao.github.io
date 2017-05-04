---
title: NexT.Hexo 配置指南
date: 2017-04-19 21:54:03
tags:
  - Hexo
  - GitHub
  - 里程碑
categories:
  - 技术
  - 博客
photo: http://iissnan.com/nexus/next/next-schemes.jpg
---

终于利用 NexT 模板基于 Hexo 配置好了博客环境，并把 Wordpress 上的几篇博文迁移至此，算是正式入住新家了。在我正式把博客发布到 GitHub Pages 之前，我还要记一下必要的安装步骤，以便日后在各台电脑上移植博客工具。

<!--more-->

# 安装

## <span id="1.1"> 安装 Hexo </span>

Hexo 的安装过程可以参考 [hexo.io](https://hexo.io/zh-cn/docs/)，简要的安装过程为：
1.  安装 [Node.js](https://nodejs.org/)
2.  安装 [Git](https://git-scm.com/)，Git for windows 的镜像在[这里](https://github.com/waylau/git-for-win)。
3.  安装 Hexo
    ```sh
    $ npm install -g hexo-cli
    ```

## 建站

安装 Hexo 完成后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```sh
$ hexo init <folder>
$ cd <folder>
$ npm install
```

## 安装插件

生成页面可能依赖一些其他插件：
*   本地搜索数据库生成器
    ```sh
    $ npm install hexo-generator-searchdb --save
    ```
*   RSS 订阅生成器
    ```sh
    $ npm install hexo-generator-feed --save
    ```
*   安装 Git 部署
    ```sh
    $ npm install hexo-deployer-git --save
    ```
其中 `--save` 选项会将插件的依赖关系写入 `package.json` 文件，方面以后用 `npm install` 命令一次安装所有依赖的插件。

# 配置

## 主文件配置

修改 `_config.yml` 中的各项自定义项，并添加 Git 部署配置：
```yml
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
```

## 主题文件安装与配置

参考 [NexT 使用文档](http://theme-next.iissnan.com/) ，安装主题并完成自定义配置。

最后，对于绑定了域名的，要在 `source` 文件夹下新建文件 `CNAME` 并写入绑定的域名，以避免访问发生错误。站点文件夹可以通过 OneDrive 进行同步，同步的内容包括主题、模板、源文件以及插件，需要用其他电脑发布博客，只需完成安装的第一步：[安装 Hexo](#1.1) 即可。

顺便提一嘴，习惯了用 LaTeX 写文档，突然间转用 Markdown 真是相当不适应，写了好几句话就是不能断行思路上是相当别扭。