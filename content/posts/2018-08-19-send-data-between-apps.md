---
title: 使用Takser在应用间传递数据
author: 记忆水晶
type: post
date: 2018-08-19T13:57:00+00:00
url: /2018/08/19/send-data-between-apps.html
views:
  - 104
categories:
  - 教程
tags:
  - IntentTask

---
使用Tasker是可以让应用间传递数据的,即使这些应用与Tasker应用没有直接联系.  
这个过程涉及到3个方面:  
1,使用Tasker启动应用A后获取应用A返回的数据.  
2,对获取的数据进行处理.  
3,把数据传递给应用B,并使其执行相应操作.  
一个适用的场景如下:  
Tasker调用二维码扫描器扫描共享单车上的二维码后,打开共享单车应用并解锁当前共享单车. 

此方法可以借助intenttask实现