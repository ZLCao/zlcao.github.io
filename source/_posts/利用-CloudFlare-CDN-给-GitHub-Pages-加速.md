---
title: 利用 CloudFlare CDN 给 GitHub Pages 加速
tags:
  - CloudFlare
  - hexo
categories:
  - 技术
  - 博客
photo: https://pics-1253593512.image.myqcloud.com/18qy/cloudflare.png
date: 2018-07-27 14:10:34
---


最近博客首页打开慢得难以忍受，百度了一下才发现是 GitHub 的部分 CDN 被 GFW DNS 污染所致。上一篇才折腾了 CloudFlare 加速 VPS，这里拿来加速 GitHub Pages 服务也是毫无问题的。由于 HTTPS 方案是对整个域名应用的，而指向 VPS 上并未部署 HTTPS 服务因此采用了 Flexible SSL 方案，这里不得不到 GitHub 个人主页的项目设置中关闭强制 HTTP。尽管这样加速已经成功，但还存在一个奇怪的小 bug，导航栏上诸如归档、分类等标签，点击后会跳转到 Http 站点，而文章链接正常。这就需要在 CloudFlare 控制台 Crypto 面板下打开 Always use HTTPS。另外，经测试，对于 DNS 而非 CDN 的解析，这一设置不起作用。Crypto 面板下还有 Automatic HTTPS Rewrites 功能，可以酌情打开。

<!--more-->
