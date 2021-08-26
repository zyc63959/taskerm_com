---
title: 用Tasker实现Android手机短信转发到Telegram
author: 记忆水晶
type: post
date: 2018-02-08T09:52:00+00:00
url: /2018/02/08/forward-sms-to-telegram.html
views:
  - 135
wpcom_likes:
  - 1
categories:
  - 教程
tags:
  - telegram
---

## 实现原理
**在Tasker中使用JavaScript代码调用API**

关键词：**调用**、**AP**I

## 1. API

格式：_https://api.telegram.org/bot123456789:AAabcdefghijklmn0fSeb6Z\_edLQOOf4KKqq/sendMessage?chat\_id=012345678&text=__短信内容_

参数值（即需要替换的内容）：_123456789:AAabcdefghijklmn0fSeb6Z_edLQOOf4KKqq_

_012345678_

### 1.1，申请一个机器人bot

a. 先在telegram中关注机器人bot：botfather

b. 关注之后发送 _/newbot_ ，botfather就会引导你一步一步创建一个新的机器人。

c. 创建之后 botfather会返回一个 token id 复制备用。

类似：_123456789:AAabcdefghijklmn0fSeb6Z_edLQOOf4KKqq_

### 1.2，获取你自己的id

a. 关注机器人bot：_getidsbot_

b. 机器人会返回一个id 类似：_012345678_ ；这个ID就是chat_id。

### 1.3，测试API是否生效

将修改后的API复制粘贴到浏览器中，如果返回的字符串中含有true ，证明API正确。

## 2. 调用

Tasker中的HTTP方法中，如果API中含有回车符，则发送的文本内容不全，所以改用js 实现HTTP post方法。

2.1. 新建Tasker任务，任意取名 比如：转发到 telegram，添加一个操作JavaScriptlet

2.2. 代码填写如下内容：


```javascript

var SMS=global(‘SMSRB’);

var url=”https://api.telegram.org/bot_123456789:AAabcdefghijklmn0fSeb6Z_edLQOOf4KKqq_/sendMessage?chat_id=_012345678_&text=”+SMS;

var method = “GET” ;// or”POST”/”PUT”/”DELETE”

var xhttp = new XMLHttpRequest();

xhttp.open( method, url, false );

xhttp.send(); //if method was”POST”, put info in the () here

if( xhttp.status == 200 ) { //successfulhttp request

var response = xhttp.responseText; }


```

注意：_1. 替换代码中的token\_id和chat\_id！_

_2. token_id前的bot不要去掉。_

最后，新建一个 收到短信 的触发条件和 转发到telegram 任务关联起来就可以了。

这样每次收到新短信，就可以在telegram上收到来自我们新建的机器人bot的短信消息。

你也许喜欢的文章:

[在Tasker中利用短信的通知实现短信内容转发到微信](https://taskerm.com/2020/03/05/forwarded-sms-to-wechat-by-tasker/)



