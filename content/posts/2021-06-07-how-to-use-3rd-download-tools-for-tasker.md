---
title: Tasker调用第三方下载工具
author: 记忆水晶
type: post
date: 2021-06-07T04:15:49+00:00
excerpt: 使用Tasker调用第三方下载工具adm和1dm
url: /2021/06/07/how-to-use-3rd-download-tools-for-tasker.html
ampforwp-amp-on-off:
  - default
categories:
  - 教程
tags:
  - download
  - idm
  - 工具
  - 脚本

---
## 前言

在Android上常用到的下载工具有ADM和1DM，下面分别列举使用 Tasker 调用这2个工具的方法和例子

使用时请注意包名：

  * adm：
      * com.dv.adm
      * com.dv.adm.pay
      * com.dv.get
      * com.dv.get.pro
  * 1dm:
      * idm.internet.download.manager.plus
      * idm.internet.download.manager
      * idm.internet.download.manager.adm.lite

## ADM

  1. shell或者adb wifi

  * 开始所有下载**am start -a com.dv.get.ACTION\_START\_ALL -n com.dv.adm.pay/.AEditor**
  * 停止所有下载**am start -a com.dv.get.ACTION\_STOP\_ALL -n com.dv.adm.pay/.AEditor**

<ol start="2">
  <li>
    发送意图（sendintent）
  </li>
</ol>

  * 操作：**android.intent.action.MAIN**
  * 类别：默认
  * Mime类型：空
  * 数据：空
  * 额外：**android.intent.extra.TEXT:下载url**
  * 额外：**com.android.extra.filename:文件名**
  * 额外：空
  * 包：**com.dv.adm.pay**
  * 类：**com.dv.adm.AEditor**
  * 目标：**Activity**（活动）

> 也可以将下载网址填入数据中而不使用com.android.extra.filename

3.  JavaScriptlet

```
    var downloadurl="https://down.qq.com/qqweb/TIM/android_apk/tim.apk",filename="tim.apk";
    sendIntent("android.intent.action.MAIN", "activity","com.dv.adm.pay","com.dv.adm.pay.AEditor","","","",["android.intent.extra.TEXT:"+downloadurl,"com.android.extra.filename:"+filename]);
```

## 1dm

  1. shell或者adb wifi
      * 开始所有下载am startservice -n idm.internet.download.manager.plus/idm.internet.download.manager.DownloadService -a idm.internet.download.manager.plus:action\_start\_all
      * 停止所有下载am startservice -n idm.internet.download.manager.plus/idm.internet.download.manager.DownloadService -a idm.internet.download.manager.plus:action\_pause\_all
  2. 发送意图（sendintent）<ol start="">
      <li>
        操作：android.intent.action.VIEW
      </li>
      <li>
        类别：默认
      </li>
      <li>
        Mime类型：空
      </li>
      <li>
        数据：下载网址
      </li>
      <li>
        额外：<strong>extra_filename:文件名</strong>
      </li>
      <li>
        包：<strong>idm.internet.download.manager.plus</strong>
      </li>
      <li>
        类：idm.internet.download.manager.Downloader
      </li>
    </ol>

  3. JavaScriptlet

```
    var downloadurl="https://down.qq.com/qqweb/TIM/android_apk/tim.apk",filename="tim.apk";
    sendIntent("android.intent.action.VIEW", "activity","idm.internet.download.manager.plus","idm.internet.download.manager.Downloader","",downloadurl,"",["extra_filename:"+filename]);
```
这2种下载工具均支持多文件下载，暂时没有找到如何使用Tasker调用多文件下载，读者朋友如果知道请留言。

参考文章

adm：<https://4pda.to/forum/index.php?showtopic=280941&st=3020>

1dm：<https://www.apps2sd.info/idmp/faq>