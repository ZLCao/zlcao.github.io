---
title: 搬瓦工服务器升级 Debian 9 stretch
tags:
  - 服务器
  - Python
categories:
  - 技术
  - VPS
photo: 'https://pics-1253593512.image.myqcloud.com/thumbnail/debian9.png'
date: 2018-07-28 00:41:12
---


近期，把搬瓦工上跑的 Debian 8 jessie 升级到了 9 stretch。第一次升级完成后，发现基于 Flask 搭建的 [xyy-gallery](https://xingyaoyao.tk/) 无法访问了，shadowsocks 也连不上，第一反应是由于 OpenVZ 内核过于老旧导致新版的 python 也不能正常运行了。于是第一时间进行了回滚（服务器重大变动之前备份一下真是个好习惯）。隔了一个月，心痒难耐，再次升级，并逐一排查了各个问题，现把解决过程记录如下。

<!--more-->

刚完成升级遇到的问题有

1. Shadowsocks 无法建立连接
2. Flask 站点无法访问
3. 静态网页也无法访问
4. [Speedtest](http://www.speedtest.cn/tp/751) 无法测速

其中 shadowsocks 出错的主要原因，是 openssl 更新到 1.1.0 版导致的。一种解决办法是修改利用 `pip` 安装的 shadowsocks 2.8.2 的源代码，具体操作方式参考[这篇文章](https://blog.lyz810.com/article/2016/09/shadowsocks-with-openssl-greater-than-110/)。这一问题官方已经做出了[修改](https://github.com/shadowsocks/shadowsocks/pull/947
)，因此，另一种比较简单的办法是直接利用 `apt-get` 命令下载新版 shadowsocks。

其他问题的成因，主要是 Debian 升级后 python 环境的变化导致。更新完成后，发现 `pip` 不能运行，setuptools 缺失导致 `easy_install` 也无法运行。最终重新安装了 python。另外，python 虚拟环境也出现问题，很多模块导入出错，需要删除虚拟环境目录重新建立。好在写了 `requirements.txt` 可以利用
```sh
$ pip install -r requirements.txt
```
一键完成安装。至于静态网页和 speedtest 的问题，简单排查后发现也是由于虚拟环境出错导致。Python web app 的虚拟环境错误导致了 Apache2 无法正常初始化。而删除 python 重装的过程中似乎又删除了 `libapache2-mod-wsgi-py3` 这一模块，重新装回即可。
