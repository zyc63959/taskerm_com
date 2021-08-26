---
title: Tasker安装一个月后的教程
author: 记忆水晶
type: post
date: 2019-06-29T01:24:00+00:00
url: /2019/06/29/what-to-do-after-firsty-month-of-installing-tasker.html
featured_image: /wp-content/uploads/2019/06/5-1561770913-480x300.jpg
views:
  - 237
wpcom_likes:
  - 2
categories:
  - 教程
tags:
  - Tasker
  - 教程
  - 进阶

---
 

### 引言 {#%E5%BC%95%E8%A8%80}

本篇文章针对使用几个月的用户，探讨Tasker的功能不足，以帮助用户更好的理解Tasker的用途.

Tasker可以实现很多自定义的功能，各种功能还可以组合成更多更大的复杂功能，的确方便了很多

但是理解了Tasker的功能有所不足，便可以更好的使用它的功能

### 一.Tasker暂时存在以下不足(随着更新，也许会逐步添加） {#%E4%B8%80tasker%E6%9A%82%E6%97%B6%E5%AD%98%E5%9C%A8%E4%BB%A5%E4%B8%8B%E4%B8%8D%E8%B6%B3%E9%9A%8F%E7%9D%80%E6%9B%B4%E6%96%B0%E4%B9%9F%E8%AE%B8%E4%BC%9A%E9%80%90%E6%AD%A5%E6%B7%BB%E5%8A%A0}

  1. Tasker并没有文件上传和文件下载模块。
  2. Tasker并不支持读屏和模拟点击(root模式下可以使用shell命令实现模拟点击)，即无法读取屏幕的文本信息，官方文档提到是涉及到信息安全，防止Tasker被滥用(tasker v5.7 支持了keyboard)。
  3. Tasker调用第三方应用时，需要应用在后台运行或者存在于缓存中。
  4. Tasker没有接收文件分享的接口,即你不能把一个文件或者消息直接传递(分享)给Tasker
  5. Tasker没有集成系统的菜单功能,即无法简单的选择文字后进行分享等操作
  6. Tasker虽然有添加部件的功能，但是这个部件只是任务的快捷方式，并没有把信息添加到桌面部件的功能

### 二.针对以上3个不足,这里分别给出几点(已知的)解决方法: {#%E4%BA%8C%E9%92%88%E5%AF%B9%E4%BB%A5%E4%B8%8A3%E4%B8%AA%E4%B8%8D%E8%B6%B3%E8%BF%99%E9%87%8C%E5%88%86%E5%88%AB%E7%BB%99%E5%87%BA%E5%87%A0%E7%82%B9%E5%B7%B2%E7%9F%A5%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95}

#### 上传有2种方法 

  * a. Tasker带有文件二进制读取功能,不过是以base64编码的,通过对其转码获取二进制.
  * b. 使用插件:[uploader][1]( [手机商店下载][2])

<blockquote class="wp-block-quote">
  <p>
    note:也许有用Java function 的方法,目前暂未找到相关代码.
  </p>
</blockquote>

#### 下载有4种方法 

a.使用 HTTP GET功能:<figure class="wp-block-image">

![Tasker的读屏，模拟点击，文件上传和下载，接收文件分享，菜单，桌面部件][3] </figure> 

HTTP get 下载图示

必填项: 服务器端口,Mime类型,输出文件.

图示是以[Android版的 TIM][4]下载链接作为示例.

b.利用JavaScript代码实现

c.利用Java function(即Java代码)<figure class="wp-block-image">

![Tasker的读屏，模拟点击，文件上传和下载，接收文件分享，菜单，桌面部件][5] </figure> 

%part是下载地址<figure class="wp-block-image">

![Tasker的读屏，模拟点击，文件上传和下载，接收文件分享，菜单，桌面部件][6] </figure> 

第二步的内容,%part2应该是文件名<figure class="wp-block-image">

![Tasker的读屏，模拟点击，文件上传和下载，接收文件分享，菜单，桌面部件][7] </figure> 

第6步的内容

d.调用第三方下载管理器

①通过发送意图调用<figure class="wp-block-image">

![Tasker的读屏，模拟点击，文件上传和下载，接收文件分享，菜单，桌面部件][8] </figure> 

%downloadurl是网址

②通过JavaScriptlet调用

<blockquote class="wp-block-quote">
  <p>
    sendIntent(“android.intent.action.MAIN”, “activity”,”com.dv.adm.pay”,”com.dv.adm.pay.AEditor”,””,””,””,“android.intent.extra.TEXT”+”:”+downloadurl,”com.android.extra.filename”+”:”+filename“<em>a</em><em>n</em><em>d</em><em>r</em><em>o</em><em>i</em><em>d</em>.<em>i</em><em>n</em><em>t</em><em>e</em><em>n</em><em>t</em>.<em>e</em><em>x</em><em>t</em><em>r</em><em>a</em>.<em>T</em><em>E</em><em>X</em><em>T</em>”+”:”+<em>d</em><em>o</em><em>w</em><em>n</em><em>l</em><em>o</em><em>a</em><em>d</em><em>u</em><em>r</em><em>l</em>,”<em>c</em><em>o</em><em>m</em>.<em>a</em><em>n</em><em>d</em><em>r</em><em>o</em><em>i</em><em>d</em>.<em>e</em><em>x</em><em>t</em><em>r</em><em>a</em>.<em>f</em><em>i</em><em>l</em><em>e</em><em>n</em><em>a</em><em>m</em><em>e</em>”+”:”+<em>f</em><em>i</em><em>l</em><em>e</em><em>n</em><em>a</em><em>m</em><em>e</em>);
  </p>
</blockquote>

或者

<blockquote class="wp-block-quote">
  <p>
    sendIntent(“android.intent.action.MAIN”,”activity”,”com.dv.adm.pay”,”com.dv.adm.pay.AEditor”,””,downloadurl,””,“com.android.extra.filename”+”:”+filename“<em>c</em><em>o</em><em>m</em>.<em>a</em><em>n</em><em>d</em><em>r</em><em>o</em><em>i</em><em>d</em>.<em>e</em><em>x</em><em>t</em><em>r</em><em>a</em>.<em>f</em><em>i</em><em>l</em><em>e</em><em>n</em><em>a</em><em>m</em><em>e</em>”+”:”+<em>f</em><em>i</em><em>l</em><em>e</em><em>n</em><em>a</em><em>m</em><em>e</em>);
  </p>
</blockquote>

或者

<blockquote class="wp-block-quote">
  <p>
    sendIntent(“android.intent.action.MAIN”,”activity”,”com.dv.adm.pay”,”com.dv.adm.pay.AEditor”,””,downloadurl,””,””);
  </p>
</blockquote>

可用的有第三方下载管理器有 adm,adm pro,idm 等等

#### 读屏和模拟点击可以使用插件或者第三方工具来实现 

a. autoinput.

b. touchtask.

c. auto.js

eg:[Auto.js脚本：蚂蚁森林收能量 星星球 京东金融签到 微信运动点赞等][9]

## 防止插件不运行的方法

  * a.在电池管理里面设置程序白名单
  * b.在桌面上添加程序部件来保活(仅适合能在桌面添加部件的程序).

#### 为Tasker添加分享接口和菜单接口,可通过以下插件实现

  * a.intentTASK
  * b.autoshare

#### 为Tasker添加桌面部件

  * a. KLWP
  * b. KWGT
  * c. Minimalistic Text

等等

<blockquote class="wp-block-quote">
  <p>
    本篇内容是不断更新的，针对每个问题，提供一种或多种解决方法；需要说明的是 不同的系统版本和不同的定制系统 均会对 方法的 有效性和稳定性产生影响。
  </p>
</blockquote>

java function 相关代码，取自于网络文件，作者未知.

初版写于：2019.02

 [1]: https://play.google.com/store/apps/details?id=com.freehaha.uploader
 [2]: \com.freehaha.uploader
 [3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/06/5-1561770913.jpg
 [4]: https://qd.myapp.com/myapp/qqteam/tim/down/tim.apk
 [5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/06/5-1561770915.jpg
 [6]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/06/5-1561770917.jpg
 [7]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/06/5-1561770929.jpg
 [8]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/06/5-1561770930.jpg
 [9]: https://github.com/e1399579/autojs