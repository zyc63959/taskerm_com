---
title: 用Tasker制作Instagram下载器
author: 记忆水晶
type: post
date: 2019-03-25T21:37:00+00:00
url: /2019/03/25/instagram-downloader.html
views:
  - 78
categories:
  - 教程
tags:
  - download
  - Instagram
  - JavaScript
  - 下载器
  - 脚本

---

> 这个Instagram下载器是用纯JS代码来实现的

整个过程其实挺简单的，无非就是通过正则表达式提取图片和视频的下载链接，然后下载下来

不过使用正则表达式的时候，有点曲折，必须把值循环出来，才可以，这点倒不如直接用Tasker自带的变量搜索替换来的简单。话不多说直接看代码。

以下是截图参考

![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress3-1554190795.jpeg "用Tasker制作Instagram下载器")![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress3-1554190795.jpeg "用Tasker制作Instagram下载器")

条件截图

![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress1-1554190805.jpeg "用Tasker制作Instagram下载器")![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress1-1554190805.jpeg "用Tasker制作Instagram下载器")

任务截图.jpg

![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress3-1554190810.jpeg "用Tasker制作Instagram下载器")![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress3-1554190810.jpeg "用Tasker制作Instagram下载器")

步骤1截图.jpg

![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress2-1554190812.jpeg "用Tasker制作Instagram下载器")![用Tasker制作Instagram下载器](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/beepress2-1554190812.jpeg "用Tasker制作Instagram下载器")

步骤2截图.jpg

说明
目前有个补丁：如果图片大于一张，第一张图片会下载2次，视频内容会连带视频封面也下载下来 
为啥不用一条JS命令而要分开呢？因为一条运行不正确，MMP