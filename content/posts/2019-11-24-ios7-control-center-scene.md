---
title: 使用Tasker制作仿iOS7控制中心
author: 记忆水晶
type: post
date: 2019-11-24T09:46:00+00:00
url: /2019/11/24/ios7-control-center-scene.html
featured_image: /wp-content/uploads/2019/11/iOS7控制中心-480x300.jpg
views:
  - 59
categories:
  - 教程

---
> 现在越来越流行使用收拾来操作手机，通过系统手势或者第三方手势软件结合Tasker可以变得更加好玩。

场景是Tasker中一个重要的组成部分，可以很方便的做出来一个图形化控制界面。

本配置是一个仿iOS7控制中心的界面，尽可能的模仿了控制中心的交互。

### 制作过程分为三个步骤：

1，场景制作 2，逻辑处理 3，触发设置

##### 1. 场景制作：

因为本配置时模仿的，所以场景界面就不需要独自设计了，直接根据各个元素的样式和功能添加到场景就可以了

##### 2. 逻辑处理：

a. 初始化变量，定义和获取初始的变量值

![定义和获取初始的变量值][1]   
定义和获取初始的变量值

b. 设置界面状态值与图标路径的对应关系 

![设置界面状态值与图标路径的对应关系][2]  设置界面状态值与图标路径的对应关系

c. 处理状态改变时的操作变化和状态显示 

![处理状态改变时的操作变化和状态显示][3] 处理状态改变时的操作变化和状态显示

##### 3. 触发设置: 在手势触发软件中设置运行Tasker任务

![在手势触发软件中设置运行Tasker任务][4] 在悬浮菜单中设置手势操作

演示视频
<video poster="https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/iOS7控制中心.jpg" autoplay="autoplay" controls="controls" width="540" height="960">您的浏览器不支持 video 标签。</video> 

配置导入链接:https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw+JP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs=&id=Project:控制中心


本次制作基于 Android 9，emui，Tasker 9制作不同的使用环境，兼容性有所不同，所使用的操作不尽相同，望周知。


[1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/iOS7控制中心.jpg
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/设置界面状态值与图标路径的对应关系.jpg
[3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/处理状态改变时的操作变化和状态显示.jpg
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/11/在悬浮菜单中设置手势操作.jpg