---
title: Tasker 如何使用 Tasker 插件以及 Tasker 第三方应用
author: 记忆水晶
type: post
date: 2020-01-14T00:39:00+00:00
url: /2020/01/14/tasker-plug-ins-and-3rd-party.html
featured_image: /wp-content/uploads/2020/01/事件插件-480x300.jpg
views:
  - 278
categories:
  - 教程

---
## 引语


> 很多人不清楚 Tasker 插件和 Tasker 第三方应用之间的区别，以及与 Tasker 的关系有何不同，其实对于使用者而言并不需要理解他们之间的区别，因为这两者在使用上的区别逐渐模糊而变得没有区别，不过本人后面几篇文章会详细介绍部分 Tasker 插件和 Tasker 第三方应用，说明下有利于读者理解之后的内容。


## 主要内容

1. 什么是 Tasker 插件，2. 什么是 Tasker 第三方应用，3. 如何使用他们，4. 常用的 Tasker 插件和第三方应用有哪些（本篇重点）。

### 什么是插件

对于使用者而言，Tasker 插件是指专门为 Tasker 添加附属功能的 Android 应用，单独使用的话无任何功能可用，关系类似于 Chrome 和 Chrome 扩展程序；Tasker 第三方应用是指本身有独立的功能可用，既可以脱离 Tasker 单独使用，也可以结合 Tasker 使用，关系类似于 Chrome 和 Chrome 应用。

### 什么是第三方应用

对于开发者而言，Tasker 插件是指专门为 Tasker 应用的功能不足或者不宜使用而设计的辅助应用；Tasker 第三方应用是指为了自己的应用添加一个可以和 Tasker 搭配使用的接口。

### 使用方式 

  1. 分为两种：作为触发条件使用和作为任务操作使用。

#### a. 作为触发条件使用： 

创建配置时选择事件（Event）或者状态（State）中的插件 (Plugin)。

![事件插件][1]  

![状态插件][2] 

#### b. 作为任务操作使用：

添加操作时选择插件 (Plugin)。

![操作类别][3]  
![操作插件][4] 
![第三方][5] 

### 常用的 Tasker 插件和第三方应用

#### 常用的Tasker插件

Tasker 插件非常多，目前常用到的 Tasker 插件有两大类：[joaomgcd][6] 作者的 auto 系列插件（程序名以 auto 开头）和 [Marco Stornelli][7] 作者的 task 系列插件（程序名以 task 结尾）。这两大类的应用功能其实很相似以至于可以把他们一一对应起来，比如：

  * [AutoTools][8] 和 [SecureTask][9] 主要功能有 系统安全设置，管理系统锁屏，管理设备 PIN，应用管理 (安装，卸载，冻结等等)，等等系统高级设置一类。
  * [AutoShare][10] 和 [IntentTask][11] 主要功能有 添加右键菜单，好用的 intent 设定，启动和管理应用快捷方式，方便 Tasker 来与其他第三方应用互动操作。
  * [AutoInput][12] 和 [TouchTask][13] 主要涉及模拟按键和手势（点击，长按，滑动等等），以及监控系统按钮和手势操作。
  * [AutoVoice][14] 和 [Tasker Now][15] 主要涉及语音助手相关的功能。

#### 常用的Tasker第三方应用

比较常用到的 Tasker 第三方应用有 KLWP,KWGT,KLCK, 睡眠追踪，绿色守护，SS,SSR, 等等。

  * Tasker 可以将 Tasker 变量传递给 KLWP,KWGT,KLCK，也可以控制加载预设；
  * Tasker 既可以监控和控制睡眠追踪的状态（睡眠状态或者退出睡眠状态）；
  * Tasker 可以通过绿色守护来休眠和唤醒全部或者选定的应用；

[Tasker wiki][16] 站列出了大量的插件和第三方应用，可供参考。

[1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E4%BA%8B%E4%BB%B6%E6%8F%92%E4%BB%B6.jpg
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E7%8A%B6%E6%80%81%E6%8F%92%E4%BB%B6.jpg
[3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E6%93%8D%E4%BD%9C%E7%B1%BB%E5%88%AB.jpg
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E6%93%8D%E4%BD%9C%E6%8F%92%E4%BB%B6.jpg
[5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E7%AC%AC%E4%B8%89%E6%96%B9.jpg
[6]: https://play.google.com/store/apps/dev?id=8102570190170276456
[7]: https://play.google.com/store/apps/dev?id=6982888636488378244
[8]: https://play.google.com/store/apps/details?id=com.joaomgcd.autotools
[9]: https://play.google.com/store/apps/details?id=com.balda.securetask
[10]: https://play.google.com/store/apps/details?id=com.joaomgcd.autoshare
[11]: https://play.google.com/store/apps/details?id=com.balda.intenttask
[12]: https://play.google.com/store/apps/details?id=com.joaomgcd.autoinput
[13]: https://play.google.com/store/apps/details?id=com.balda.touchtask
[14]: https://play.google.com/store/apps/details?id=com.joaomgcd.autovoice
[15]: https://play.google.com/store/apps/details?id=com.balda.taskernow
[16]: http://tasker.wikidot.com/plug-ins-and-3rd-party