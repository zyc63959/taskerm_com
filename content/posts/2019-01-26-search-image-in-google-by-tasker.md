---
title: 使用Tasker实现以图搜图
author: 记忆水晶
type: post
date: 2019-01-26T21:22:00+00:00
url: /2019/01/26/search-image-in-google-by-tasker.html
views:
  - 105
categories:
  - 教程
tags:
  - IntentTask

---
## 作用 

手机上的Google image 搜索没有提供手机版，这个以图搜索配置解决这个问题(当然你也可以用PC端的搜索引擎)。 

## 原理

将图片上传到一个图床内并获取外联，使用Google image搜索该网址。

## 插件 

IntentTask（作用：添加一个分享到的入口） 

## 具体方法 

打开图片后将图片分享到IntentTask，IntentTask获取到图片信息后，传递给tasker，tasker处理图片后上传图片并获取外联网址，并进行搜索。 

## 过程 

  1. 在intenttask内新建一个 command 命名为 “以图搜图”。
  2. 在tasker内添加配置，过程省略。[点我导入](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv%2Fcr1krqlca25FgFK7KKdWs%3D&id=Profile%3A%E4%BB%A5%E5%9B%BE%E6%90%9C%E5%9B%BE)

