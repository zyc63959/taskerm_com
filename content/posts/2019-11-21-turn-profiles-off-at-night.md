---
title: 夜间关闭大部分的Tasker配置来节省电量
author: 记忆水晶
type: post
date: 2019-11-21T10:01:00+00:00
url: /2019/11/21/turn-profiles-off-at-night.html
featured_image: /wp-content/uploads/2019/11/配置预览-480x300.jpg
views:
  - 116
categories:
  - 教程

---
## 引语

> 不知道是什么原因最近Tasker的耗电量一直居高不下


## 原理

因为Tasker内置了很多对Tasker自身的设置，比如: 禁用Tasker，禁用Tasker配置，设定Tasker偏好等等，通过这些操作都可以达到节省电量的目的；所以对自己的配置进行了定时管理，处于夜间的时候关闭大部分的配置以节省电量消耗。

## 步骤

设计配置非常简单，用Tasker本身的操作也不会很复杂。不过这里用JavaScript来代替处理逻辑部分。  
以下参考图示即可自主完成操作 


![配置预览][1]
配置预览
![禁用配置][2]
禁用配置
![禁用配置代码][3]
禁用配置代码![在退出任务中设定原来的配置可用][4] 

在退出任务中设定原来的配置可用
![退出任务的代码][5]
退出任务的代码

## 说明

创建好之后记得把该配置锁定，以免造成问题

## 附上配置连接

<https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv%2Fcr1krqlca25FgFK7KKdWs%3D&id=Profile%3ATasker%E9%85%8D%E7%BD%AE%E5%A4%9C%E9%97%B4%E5%85%B3%E9%97%AD>

[1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/%E9%85%8D%E7%BD%AE%E9%A2%84%E8%A7%88.jpg
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/%E7%A6%81%E7%94%A8%E9%85%8D%E7%BD%AE.jpg
[3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/%E7%A6%81%E7%94%A8%E9%85%8D%E7%BD%AE%E4%BB%A3%E7%A0%81.jpg
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/%E5%9C%A8%E9%80%80%E5%87%BA%E4%BB%BB%E5%8A%A1%E4%B8%AD%E8%AE%BE%E5%AE%9A%E5%8E%9F%E6%9D%A5%E7%9A%84%E9%85%8D%E7%BD%AE%E5%8F%AF%E7%94%A8.jpg
[5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/%E9%80%80%E5%87%BA%E4%BB%BB%E5%8A%A1%E7%9A%84%E4%BB%A3%E7%A0%81.jpg