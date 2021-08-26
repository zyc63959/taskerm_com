---
title: 使用 Tasker 实现控制手机发短信
author: 记忆水晶
type: post
date: 2020-08-09T04:03:01+00:00
url: /2020/08/09/used-tasker-to-send-sms.html
views:
  - 146
ampforwp-amp-on-off:
  - default
categories:
  - 配置
tags:
  - JavaScript
  - 即时通讯
  - 发送短信
  - 配置

---
## 引言 

不知道为啥国内大多数的互联网公司为了验证手机号都是 互联网公司发验证码短信到个人手机 ，偏偏**腾讯**就不一样，验证码短信需要个人向腾讯发送；更奇葩的是，国内没有一家面向普通用户的即时通讯应用服务商可以跟**腾讯**竞争。所以遇到手机没带又需要发送短信的时候就比较麻烦。 [Tasker 配置教程站][1]

## 主要内容 

之前的文章[利用 Tasker 实现将短信转或者未接来电信息发到微信，钉钉，TG 等即时通讯聊天工具][2]，这样不必带多余的手机也可以查收收手机短信或者未接来电信息；本篇说下如何利用手机中的 QQ ，微信等即时聊天工具应用控制手机发送短信；(记忆水晶)这样就用 Tasker 完整实现手机短信的收发工作，完美闭环。

## 原理 

通过（电脑端或者手机端的） QQ 发送信息到受控端的手机 QQ ， Tasker 检测到 QQ 的特定通知内容，启动发送短信的任务。

## 使用条件与场景 

  1. 准备一部手机并安装有 QQ 或者微信等即时通讯工具应用。
  2. 手机安装 Tasker 应用，并给予短信和通知相关的权限。

## Tasker 配置步骤 

  1. 添加触发条件：以事件中的界面分类下的通知为触发。
  2. 添加任务：以代码中的JavaScriptlet作为执行的操作。  
![ Tasker 触发条件为事件中的通知，操作为代码中的JavaScriptlet][3]  
    视频演示步骤： document.getElementById(&#8220;spkj&#8221;).style.height=document.getElementById(&#8220;spkj&#8221;).scrollWidth*0.76+&#8221;px&#8221;; 

&nbsp;代码
```
    const cmd = evtprm[2] || exit(flashLong(`无法获取通知内容`));
    const arr = /\!([0-9]+)\^(.+)\$/gi.exec(cmd);
    if (arr.length) sendSMS(arr[1], arr[2], true);
```

## 使用方式 

通过 QQ 或者微信发送以下格式的代码  
`!接收者号码^短信内容$`  
例如：把 0000 发送给 100086 的命令就是&nbsp;`!10086^0000$`。

> 请注意：!^$这三个字符均为半角英文符号。  
> 当然你也可以使用自己喜欢的符号字符，只需要将其按照顺序替换即可。

本篇代码跟利用 Tasker 实现短信转发到微信的代码结合，可以将短信发送的结果返回到 QQ 或者微信中

## 说明 

  * 所有者程序可以选择 QQ 或者微信等第三方程序，也可以不选，建议选一个或者多个。
  * 本篇中的代码如与图片或者视频中的代码不同，不影响使用。

## 排错指南 

  1. 检查 Tasker 是否处于运行状态。
  2. 检查 Tasker 是否可以获取到应用通知内容，如果配置运行不正常多半是这个的原因。
  3. 检查 Tasker 是否有发送短信的权限。

 [1]: //taskerm.com
 [2]: https://taskerm.com/2018/12/22/forwarded-sms-to-wechat/
 [3]: //oss.Taskerm.com/2020/08/Tasker%E4%BB%BB%E5%8A%A1%E6%93%8D%E4%BD%9C%E4%BB%A3%E7%A0%81JavaScriptlet.jpg!default