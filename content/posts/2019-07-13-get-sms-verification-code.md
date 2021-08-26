---
title: 用Tasker识别并提取短信中的验证码
author: 记忆水晶
type: post
date: 2019-07-13T09:19:00+00:00
url: /2019/07/13/get-sms-verification-code.html
featured_image: /wp-content/uploads/2019/07/get-sms-verification-code-480x300.jpg
views:
  - 249
categories:
  - 教程
tags:
  - code
  - Tasker
  - 实例
  - 配置
  - 验证码

---
> 短信验证码 使用的是[https://github.com/zhidao8/SmsCodeHelper](https://github.com/zhidao8/SmsCodeHelper)的源码

## 该源码有如下特点:

1. 该源码适配了中日英三种语言(尤其是支持google验证码),感觉应该可以应付目前各种样式的验证码了.

2. 源码还支持自定义正则表达式提取(这个我删除了,orz)

3. 除了验证码还支持快递取件码(不好意思这个我也没加)&nbsp;

## 目前该配置的具体功能是:

在收到验证码短信后,提示验证码并自动复制验证码.

![get-sms-verification-code](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/07/get-sms-verification-code.jpg)

verification code 最后附上配置链接:[提取短信验证码](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw+JP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs=&id=Profile:%E6%8F%90%E5%8F%96%E7%9F%AD%E4%BF%A1%E9%AA%8C%E8%AF%81%E7%A0%81)
链接需要安装 google play套件,需要登录Google账号.

## 预计后续会加入的功能:

1. 提取快递取件码

2. 使用悬浮窗来提示验证码

3. 一段时间后清理眼贴板内容


注意：
单独使用Tasker是无法实现全自动填写验证码的,需要用到autoinput插件或者touchtask插件.

`该配置不适合360手机和魅族手机等无法读取验证码短信的手机`
