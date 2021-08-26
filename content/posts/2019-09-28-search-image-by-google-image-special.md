---
title: 使用Tasker实现 以图搜图（酷安版）
author: 记忆水晶
type: post
date: 2019-09-28T21:20:00+00:00
url: /2019/09/28/search-image-by-google-image-special.html
views:
  - 126
categories:
  - 教程
tags:
  - Tasker
  - 以图搜图
  - 实例
  - 配置

---
## 引语


    酷安现在已经是搞基社区了，年轻人的各种趣事都可以分享，酷图也是很好的板块，各种漂亮妹子图，/逃，看的流口水了，会不会想知道图出处或者更高分辨率的图片呢？


## 说明

本配置可以通过分享酷安图片的方式，来找到图片的出处。

  * 配置用的网络服务：

  1. [https://sm.ms][1]&nbsp;图床
  2. [https://image.baidu.com][2]&nbsp;图片搜索引擎

  * 本配置用到的插件：intentTask

## 原理

通过intentTask获取到图片的路径，并将其上传到sm.ms的图床后得到图片url，然后用图片搜索引擎 百度图片搜索 找到图片来源。

## 创建步骤

配置创建步骤：

  1. 安装插件intentTask，并建立一个名称为&nbsp;`以图搜图（酷安版）`的命令（command）
  2. 在Tasker新建一个名称为&nbsp;`以图搜图（酷安版）`&nbsp;的配置
  3. 触发条件 选择&nbsp;`插件`&nbsp;中的&nbsp;`intentTask`
  4. 添加如下图所示 任务

## 使用步骤

使用步骤：  
打开酷安，选择一张图片，点击分享图片到intentTask中的&nbsp;`以图搜图（酷安版）`，系统会自动打开浏览器，从而找到相应的图片信息

视频演示:<figure class="wp-block-video"><video controls src="https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/10/%E4%BB%A5%E5%9B%BE%E6%90%9C%E5%9B%BE%E6%BC%94%E7%A4%BA%E8%A7%86%E9%A2%91.mp4"></video></figure> 

导入链接： <a rel="noreferrer noopener" href="https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv%2Fcr1krqlca25FgFK7KKdWs%3D&id=Profile%3A%E4%BB%A5%E5%9B%BE%E6%90%9C%E5%9B%BE%EF%BC%88%E9%85%B7%E5%AE%89%E7%89%88%EF%BC%89" target="_blank">https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv%2Fcr1krqlca25FgFK7KKdWs%3D&id=Profile%3A%E4%BB%A5%E5%9B%BE%E6%90%9C%E5%9B%BE%EF%BC%88%E9%85%B7%E5%AE%89%E7%89%88%EF%BC%89</a>

[1]: https://sm.ms/
[2]: https://image.baidu.com/