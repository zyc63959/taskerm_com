---
title: Tasker无法调用插件或者无法运行第三方应用的解决方法
author: 记忆水晶
type: post
date: 2019-11-29T14:11:00+00:00
url: /2019/11/29/how-to-solve-the-problem-that-tasker-cannot-call-plugins-or-cannot-run-third-party-applications.html
featured_image: /wp-content/uploads/2019/11/运行应用程序-Tasker-480x300.jpg
views:
  - 133
categories:
  - 教程
tags:
  - 3rd-app
  - plugins

---
## 问题原因

这个问题其实已经存在5,6年了,自Android&nbsp;5.0发布以来Tasker无法调用插件或者无法运行第三方应用的现象越来越突出.  
一个原因也许是,Android&nbsp;4.0-4.4 世代手机设备大多已经root,尤其是玩Tasker的.国产手机不root压根就安装不了Tasker早期版本.  
Tasker使用者也越来越多  
Tasker作者之前说原因是Google play的政策影响造成的.这个理由本人持怀疑态度.

## 问题分析

### Tasker插件 

我们先来看下Tasker是如何调用插件来协助完成任务的.  
`From version 5.1.5b, Tasker will use IntentServices to call plugins if available. This will make plugin integration faster and more reliable.`  
`Add Services in the manifest with the same com.twofortyfouram.locale.intent.action.FIRE_SETTING and com.twofortyfouram.locale.intent.action.QUERY_CONDITION intent filters as your existing broadcast receivers and make sure they're exported (android:exported="true")`
从摘抄中可以看出这个是Tasker通过服务发出消息给插件来执行各种任务,插件通过自身已经设置的广播接收器来接收信息,从而来执行相应的任务.  
应用与应用间的消息传递,需要插件自身在手机系统中处于不被杀死的状态才能接收到信息,否则插件既不能收到消息也不能自启动,就无法执行Tasker发出的命令.  
这个过程中Tasker仅仅做了一件事,发一条信息给插件;至于插件能不能收到信息,Tasker无法保证.

### 第三方应用 

在讲Tasker启动第三方应用之前,我们先来看看通常见到的情况是怎么样的.

a.在应用中的一个界面中点击一个按钮,跳转到该应用中的另一个界面.

b.在应用中的一个界面中点击一个按钮,跳转到第三方应用中的一个界面.

c.没有执行任何操作,应用自行跳出来.(比如在微信Windows客户端中点击登录按钮,手机微信自行跳出确认界面)

## 举例说明

以抖音下载器这个配置为例:在抖音客户端界面复制到抖音短链接,Tasker检测到系统剪贴板发生变化,并且变量值符合条件约束,然后执行下载任务,ADM Pro开始下载抖音短视频.  
这个过程中,如果 Tasker后置,ADM Pro 未运行,那么这种情形不符合上面的三种情形,此时ADM Pro便不能下载文件.

## 问题隐蔽性

很多时候我们明明测试的没有问题,但是配置却运行不正常,也是这个原因:测试的时候Tasker前置,可以正常启动第三方应用程序,自动运行的时候Tasker后置,此时如果第三方应用未在后台运行,那么很可能无法正常启动应用.

所以,要想操作执行正常,对于插件来说,必须处于运行状态,因为即便Tasker前置,如果插件被系统杀死,也是无法正常执行操作的.  
而对于第三方应用来说,Tasker前置,应用前置,应用后置,均可以让操作正常执行.大部分情况下无法简单判断程序是否后台运行,所以通常是让Tasker前置.

## 让Tasker前置的方法有两种

### 启动Tasker应用

使用启动应用程序这个操作来运行Tasker.

### 创建空白场景

使用场景来模拟Tasker应用程序前置

如图所示创建配置<figure class="wp-block-image">

![启动应用-Tasker][1] </figure>

[1]: http://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/%E8%BF%90%E8%A1%8C%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F-Tasker.jpg