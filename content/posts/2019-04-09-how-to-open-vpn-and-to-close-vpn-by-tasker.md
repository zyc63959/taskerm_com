---
title: 使用Tasker自动开关VPN工具
author: 记忆水晶
type: post
date: 2019-04-09T21:18:00+00:00
url: /2019/04/09/how-to-open-vpn-and-to-close-vpn-by-tasker.html
featured_image: /wp-content/uploads/2019/04/6-1554883436-480x300.jpg
views:
  - 311
wpcom_likes:
  - 1
categories:
  - 教程
tags:
  - auto
  - toggle
  - vpn

---
> 本篇文章适合 Tasker 6.2及以上版本
> 适用VPN有  SS,SSR,SSRR,openVPN,v2rayNG

能用的科学上网工具少之又少，免费好用的更是凤毛麟角。  
一些免费开源的工具支持Tasker，用起来真的很爽。  
下面说下以SSRR为例如何使用自动开启和关闭吧

1.  自动开启

*   a.按应用程序开启  
点击新建配置按钮，选择触发类型：应用程序，

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/6-1554883436.jpeg "使用Tasker自动开关科学上网工具")

选择应用程序

在应用选择里面选择需要的程序，下面的活动（activity）、服务（service）、反转、全部，默认只选中 **活动（activity）**就可以了，

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/3-1554883436.jpeg "使用Tasker自动开关科学上网工具")

选择程序

选好之后点击返回按钮，在弹出的任务菜单选项中，选择新建任务，

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554883437.jpeg "使用Tasker自动开关科学上网工具")

新建任务

任务名可以不填写，点击右边的√符号，点击添加操作按钮，在操作菜单选项中选择**插件**

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554883437.jpeg "使用Tasker自动开关科学上网工具")

插件

中的**SSRR**，

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/8-1554883437.jpeg "使用Tasker自动开关科学上网工具")

SSRR

在操作修改窗口选择点击右侧的配置按钮，

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/5-1554883437.jpeg "使用Tasker自动开关科学上网工具")

配置按钮

打开**启动服务**，选中**使用当前配置**（不选会出错）后

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554883438.jpeg "使用Tasker自动开关科学上网工具")

点击两个按钮

自动返回操作修改窗口，点击返回两次

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/5-1554883438.jpeg "使用Tasker自动开关科学上网工具")

点击两次

，在Tasker主窗口点击**保存按钮√**，

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/0-1554883438.jpeg "使用Tasker自动开关科学上网工具")

保存

这样一个按照应用程序开启SSRR的配置就完成了。

*   b.按时间段开启  
点击新建配置按钮，选择触发类型：时间，设定好开始和结束的时间点，选好之后点击返回按钮，_在弹出的任务菜单选项中。。。_接下来的内容参考上一段。

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/4-1554883440.jpeg "使用Tasker自动开关科学上网工具")

设置时间段


2.自动关闭

*   a. 按应用程序关闭  
①程序关闭时关闭

可以设定退出任务，在任务中添加network access操作

②程序开启时关闭

新建配置，选择应用程序

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/8-1554883442.jpeg "使用Tasker自动开关科学上网工具")

选择应用程序

任务中添加操作network access

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554883444.jpeg "使用Tasker自动开关科学上网工具")

network access

返回保存

*   b. 按时间段关闭

如果晚上不用了可以让其夜间自动关闭  
3个触发条件：时间段，息屏，网络连接

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554883449.jpeg "使用Tasker自动开关科学上网工具")

夜间关闭

![使用Tasker自动开关科学上网工具](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/3-1554883450.jpeg "使用Tasker自动开关科学上网工具")

任务


最后分享下配置导入链接

1.  [启动](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs%3D&id=Profile%3AVPN%E5%90%AF%E5%8A%A8v1)
2.  [关闭](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs%3D&id=Profile%3AVPN%E5%A4%9C%E9%97%B4%E5%85%B3%E9%97%ADv1)
3.  [夜间定时关闭](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs%3D&id=Profile%3A%E5%85%B3%E9%97%ADVPNv1)