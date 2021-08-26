---
title: Tasker实现精准定时执行的方法
author: 记忆水晶
type: post
date: 2019-04-17T21:30:00+00:00
url: /2019/04/17/time-point.html
views:
  - 144
wpcom_likes:
  - 1
categories:
  - 教程
tags:
  - 时间段
  - 时间点

---
## 时间段的缺点

> Tasker虽然有按照时间段执行任务的方法，但是这个时间据说并不很精准，有时间差。  
> 很多人都希望可以定时运行任务，有时间差的时间段并不能满足需求，所以这里谈一下精准定时的方法，希望对大家有用。

## 时间段的用途

时间段这个触发条件一般是用来限制触发时间的，常常作为用于省电考虑的附加条件，不适合单独做触发条件。

## 精准定时的原理

精准定时的原理是利用系统的android.intent.action.TIME_TICK这个意图来实现的，通过设定触发条件为接收意图，那么接下来选定的任务就会在系统时间的分钟改变时得到执行。就好像，每过一分钟，系统状态栏的时间栏就会更新一次一样。

这个可以精确到分，如果想要精确到秒，可以使用等待`wait`这个操作

## 说明

如果感觉比较费电，可以和时间段，状态等类型的条件一起使用。 最后分享一个做好的配置[整点同步](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw+JP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs=&id=Profile:白天整点同步)以供参考。