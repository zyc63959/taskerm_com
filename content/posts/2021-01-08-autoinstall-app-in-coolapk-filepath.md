---
title: 免root实现酷安应用静默安装和更新–Tasker教程
author: 记忆水晶
type: post
date: 2021-01-08T04:05:00+00:00
url: /2021/01/08/autoinstall-app-in-coolapk-filepath.html
views:
  - 447
wpcom_likes:
  - 5
categories:
  - 教程

---
# 免root实现酷安应用静默安装和更新&#8211;Tasker配置教程站

> 大家都知道在 root 下，酷安是可以实现静默安装的，对于没有root的同学很不友好，这里教大家如何用tasker实现免root下的酷安应用静默安装和更新

## 使用条件：

    1. 使用最新版本的 Tasker，目前最新版是 5.11.12-rc
    2. 给 Tasker 添加 adb wifi 权限

## 酷安设置

    1. 依次打开酷安→设置→下载安装，下滑到页面底部，将`自动开始安装`关闭
    2. 复制下自定义下载目录的路径

    Android/data/com.coolapk.market/files/Download/

## 创建tasker配置

    1.  **触发条件:**

依次点击 新建（加号）→文件→文件被修改→文件下面填写刚复制的内容，然后返回。

    2.  **任务创建:**

  * 依次点击 新建任务→新建操作（加号）→任务→if

在if操作的界面中 左边填写 `%evtprm2`，右边填写 `MovedTo`，然后返回。

  * 添加操作变量搜索替换

其中，变量 填写 `%evtprm1`  
搜索 填写`([^/\\\|:""\*\?]+\.\w+$)`  
选中`只匹配一次`复选框  
将匹配存储到 填写 `%filename`  
然后返回

  * 添加操作adb wifi，命令内填写
```
    cp %evtprm1 /data/local/tmp/%filename
    pm install -r /data/local/tmp/%filename
    rm /data/local/tmp/%filename
    rm %evtprm1
```
超时右滑到最大值，然后返回

    3. **保存配置**

现在打开酷安连续下载几个应用都会静默安装到手机上了。