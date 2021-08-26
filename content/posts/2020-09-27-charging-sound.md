---
title: 在Android手机上实现充电提示音的视频效果
author: 记忆水晶
type: post
date: 2020-09-27T13:00:00+00:00
url: /2020/09/27/charging-sound.html
views:
  - 146
wpcom_likes:
  - 2
categories:
  - 配置
tags:
  - 充电提示音
  - 充电视频
  - 场景
  - 配置

---
# 在Android手机上实现充电提示音的视频效果

## 使用tasker创建配置的优势

建议使用Tasker来实现充电提示音的效果：

  1. 操作简便
  2. 稳定可靠
  3. 教程多，素材多，降低使用门槛，节省折腾时间
  4. 对老旧系统友好，可支持Android 2.3以上版本
  5. 支持车机，手表等Android系统设备
  6. 配置文件可导入导出和共享出来，便于分享交流

## 准备条件：

  1. Android手机一部（Android 4.0系统以上，Android 2.3以下的不确定是否可行）
  2. Tasker应用：在此处下载各系统支持的Tasker版本和相关使用方法说明：[Tasker下载][1]
  3. 充电提示音视频素材文件：<http://link.taskerm.com/miku-live-wallpaper> 提取码：0000

## 创建配置步骤：

该配置的类型是工程（什么是配置文件：）引用  
主要包含三个部分：触发条件，任务，场景

  1. 创建场景  
    a. 在配置文件、任务、场景、变量四个选项卡中，选中上面的场景选项卡  
    b. 点击底部右侧的加号开始新建场景  
    c. 填写场景名字（必填）后点击旁边的对号√进入场景编辑界面  
    d. 点击右上角的汉堡菜单，选择属性  
    e. 在属性几何学下面的框里填写两个 10000或者尽可能大的数字  
    f. 返回后点击放大镜  
    g. 添加元素“视频”：点击底部的加号，可以看到对话框，向上滑动到底部，选中“视频”  
    h. 设置视频元素属性：
    
        ①将几何学中的四个数字依次填写将几何学中的四个数字依次填写 0,0，10000或者尽可能大的数字，10000或者尽可能大的数字
        ②点击源右边的放大镜，选择一个准备好的充电提示音视频文件
    
    i. 返回到Tasker主界面，点击上面的对号保存一下

  2. 创建任务  
    a. 在配置文件、任务、场景、变量四个选项卡中，选中上面的 任务 选项卡  
    b. 点击底部右侧的加号开始新建场景  
    c. 填写任务名字（必填）后点击旁边的对号√进入 任务编辑 界面  
    d. 点击右下角的加号添加操作，依次选中 场景，显示场景 进入操作修改界面  
    e. 设置操作属性
    
        ①名称：填写你创建的场景名称或者点击右侧放大镜选中你创建的场景名称
        ②显示为：选择3个对话类型的任意一个（在本配置中，选哪种对话效果并无明显区别）
    
    f. 返回到任务编辑界面，点击右下角的加号添加操作，依次选中 任务，等待 进入操作修改界面  
    g. 设置操作属性
    
        ①通过点击向上和向下的箭头选择视频的秒数（S）
        ①通过点击向上和向下的箭头选择视频的毫秒数（MS）
        eg:如果视频时长为：3.2秒，则毫秒数选择200、秒数选择3
    
    h. 返回到任务编辑界面，点击右下角的加号添加操作，依次选中 场景，删除场景 进入操作修改界面  
    i. 设置操作属性
    
        ①名称：填写你创建的场景名称或者点击右侧放大镜选中你创建的场景名称
    
    j. 返回到Tasker主界面，点击上面的对号保存一下

  3. 创建配置  
    a. 在配置文件、任务、场景、变量四个选项卡中，选中上面的 配置 选项卡  
    b. 点击底部右侧的加号开始新建触发条件（噫，怎么不是配置呀）  
    c. 在弹出的界面中依次选中：状态、电源、电源  
    d. 点击返回后，在弹出的界面中选中你创建的任务名称  
    e. 点击上面的对号保存一下

这样一个非常简单的充电提示音视频版就创建好了，现在插上电源试试效果吧！  
演示效果：

你以为就这样结束了吗？然而并没有。

## 防杀

这个是很多使用者们都容易忽视的部分

  1. 防止系统清理：进入系统最近任务界面，点击Tasker应用旁边的小锁，锁定Tasker不被系统清理
  2. 忽略电池优化：依次打开系统设置，应用和通知，应用管理，设置，特殊访问权限，忽略电池优化（直接在设置搜索栏搜索电池也能找到），允许忽略Tasker
  3. 设置启动管理：依次打开系统设置，电池，启动管理，关闭Tasker自动管理后弹出的对话框中选中：允许自启动，允许关联启动，允许后台活动

![Tasker-防杀][2] 

## 权限设置

  1. 开启悬浮窗权限（必须）
  2. 开启存储权限

更详细的权限设置内容参考这里：[Tasker权限设置][3]

## 高阶玩法

如果你感觉这个配置效果单一，还可以

  1. 添加断电提醒
  2. 添加音频视频协同提醒
  3. 设置不同时间段显示不同提示

## 结语

  1. Tasker作为Android系统创世之初就诞生的自动化管理应用，功能强大自不必说，功能更新特别快，早买不亏。
  2. Tasker的简中翻译一言难尽，希望英文较好的同学多多提供翻译支持，供小白们更方便使用。[Tasker官方简中翻译][4]
  3. 除了创建有趣的配置外，Tasker是一款真正意义上可以提高生产力的工具。

Tasker正版用户配置导入链接：<http://link.taskerm.com/charging-video>

 [1]: https://taskerm.com/tasker-download.html
 [2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/10/%E5%90%AF%E5%8A%A8%E7%AE%A1%E7%90%86.jpg!default "Tasker-防杀"
 [3]: https://taskerm.com/2020/01/31/how-to-enable-all-permissions-and-services-required-by-tasker-in-pc.html
 [4]: http://link.taskerm.com/translate-tasker-coolapk