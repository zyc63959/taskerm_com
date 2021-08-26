---
title: USB连接电脑时自动打开USB网络共享
author: 记忆水晶
type: post
date: 2020-06-17T11:31:54+00:00
url: /2020/06/17/usb-connected-turn-usb-ethernet-on.html
featured_image: https://oss.taskerm.com/2020/06/tasker-usb.jpg
views:
  - 250
wpcom_likes:
  - 1
categories:
  - 配置
tags:
  - Ethernet
  - USB
  - 实例
  - 配置

---
![usb](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/07/tasker-usb.jpg)

usb

## 背景

最近家里没宽带可用了，暂时拿手机移动网络顶上，每次打开USB网络共享（USB Ethernet）都要经过好几个步骤，也没有Android系统的快捷操作可以一步执行（WIFI热点倒是可以），故做出来这个配置。

## 说明

其实这个配置挺实用的，为啥现在才做出来呢？早先利用Tasker打开USB网络共享是需要root权限的，现在新版本的功能更强大，可以在没有root权限的设备中执行更多的操作和命令。

本配置的结构相当简单，由一个触发条件和一个操作组成

## 配置结构

配置名称：USB连接电脑时自动打开USB网络共享

## 使用条件

  1. 需要Tasker为5.9.2及以上的版本
  2. 需要在电脑上开启 ADB WIFI
  3. 基于Android 8.0 EMUI 测试，理论上适用于所有的系统

## 配置连接

  1. 配置百度网盘链接：  
    <http://link.taskerm.com/usb>
  2. 提取码：923x