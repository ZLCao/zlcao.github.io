---
title: Hipaper 主题配置心得
tags:
  - Hexo
  - GitHub
categories:
  - 技术
  - 博客
photo: >-
  https://raw.githubusercontent.com/iTimeTraveler/hexo-theme-hipaper/master/source/preview/hipaper-preview.png
date: 2017-05-02 00:14:00
---


五一在家，研究了一下 Hexo 的 [hipaper](https://github.com/iTimeTraveler/hexo-theme-hipaper) 主题。这是我在官网上第一眼看中的主题，当初由于对 Hexo 不熟悉，直接使用遇到了不少问题，因此选择了中文文档十分详细的 NexT 主题作为替代。随着对 Hexo 一些文件配置的逐步深入，并查看了项目 issues，我再次尝试为博客适配这个主题。

Hipaper 主题主要有以下几个问题需要解决：
1.  分类和标签页面错误
2.  标题中英文字体比中文高出很多
3.  顶部副标题不显示
4.  边栏社交图标数目太少
5.  不知道怎样生成文章头图

<!--more-->

# 分类和标签页面

分类和标签页面需要在相应的页面 `index.md` 文件中插入 `layout` 属性：
```md
layout: "categories/tags"
```

# 中英文字体问题

这个问题主要是英文 oswald 字体与中文雅黑字体不匹配造成的，可以通过替换字体的办法解决。参考作者的另一个主题 [hiero](https://github.com/iTimeTraveler/hexo-theme-hiero)，用其中的 yanone 字体进行替换。具体方法是到项目主页分别搜索这两个字体，找到相关文件，进行修改和替换。

# 顶部副标题

此主题顶部副标题显示的是 `_config.yml` 文件的 `description` 属性，而非 `subtitle` 属性。

# 边栏社交图标

原本设计的社交图标是一行六个，自己凑了五个就再也凑不出了。另外，在排满六个图标的情况下，最后一个图标右侧还有一小段空隙。我们打开 `source/css/fashion.css` 文件，找到 `.widget-social-icons` 相关代码，作如下修改：
```diff
/* Widget Social Icons */
.widget-social-icons li {
	float: left;
-	margin: 5px 10px 5px 0;
+	margin: 5px 5px 5px 5px;
	text-align: center;
	}
.widget-social-icons li a {
	display: block;
	}
.widget-social-icons li a [class^="fa"]:before {
-	width: 40px;
+	width: 50px;
	margin: 0;
	color: #fff;
-	font-size: 20px;
-	line-height: 40px;
+	font-size: 30px;
+	line-height: 50px;
	background: #333;
	}
.widget-social-icons li a:hover [class^="fa"]:before {
	background: #1fa0ae;
	}
```

# 文章头图

文章头图可以是单张图片，也可以是一组图片组成的相册，相册可以点开以查看。单张图片的插入方法是
```md
photo: <image_url>
```
相册的插入方法与之类似
```md
photos:
  - <image_url_1>
  - <image_url_2>
  - ...
```
