---
title: 如何在PC端一次性开启Tasker的所有权限和服务
author: 记忆水晶
type: post
date: 2020-01-31T00:50:26+00:00
url: /2020/01/31/how-to-enable-all-permissions-and-services-required-by-tasker-in-pc.html
keywords: 写安全,adb wifi,监听音量键,音量键长按,音量键触发,日志,Tasker服务,Tasker权限,Tasker电池优化,Tasker自启动,Tasker杀后台,普通权限,特殊权限,ADB over TCP Tasker,Tasker所有的权限,adb shell,tasker adb shell,tasker adb wifi,WRITE_SECURE_SETTINGS,DUMP,READ_LOGS,SET_VOLUME_KEY_LONG_PRESS_LISTENER,SET_MEDIA_KEY_LISTENER,应用启动管理,电池优化,通知使用权,辅助应用,设备管理器
description:在安卓手机上一次开启Tasker所有的权限，包含普通权限和特殊权限
views:
  - 397
wpcom_likes:
  - 10
ampforwp-amp-on-off:
  - default
categories:
  - 教程
tags:
  - adb
  - services
  - 服务
  - 权限

---
## Tasker需要开启很多服务和获取很多权限

通过下面的命令可以详细获取Tasker相关的权限和服务

```adb shell dumpsys package net.dinglisch.android.taskerm```

也可以用下面的命令将所有显示的信息保存到文本文件中

```adb shell dumpsys package net.dinglisch.android.taskerm >tasker.txt```

## 权限有普通权限和特殊权限

大部分权限可以手动通过设置来打开,一部分特殊权限需要使用adb授权.

### 获取普通权限的方法

#### 安装Tasker后用adb获取

可以通过下面的代码获取

```adb shell pm grant net.dinglisch.android.taskerm android.permission.PACKAGE_USAGE_STATS
adb shell pm grant net.dinglisch.android.taskerm android.permission.BODY_SENSORS
adb shell pm grant net.dinglisch.android.taskerm android.permission.WRITE_CALL_LOG
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_CALL_LOG
adb shell pm grant net.dinglisch.android.taskerm android.permission.RECEIVE_SMS
adb shell pm grant net.dinglisch.android.taskerm android.permission.WRITE_EXTERNAL_STORAGE
adb shell pm grant net.dinglisch.android.taskerm android.permission.RECORD_AUDIO
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_PHONE_STATE
adb shell pm grant net.dinglisch.android.taskerm android.permission.SEND_SMS
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_SMS
adb shell pm grant net.dinglisch.android.taskerm android.permission.ACCESS_FINE_LOCATION
adb shell pm grant net.dinglisch.android.taskerm android.permission.ACCESS_COARSE_LOCATION
adb shell pm grant net.dinglisch.android.taskerm android.permission.CAMERA
adb shell pm grant net.dinglisch.android.taskerm android.permission.PROCESS_OUTGOING_CALLS
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_CONTACTS
adb shell pm grant net.dinglisch.android.taskerm android.permission.WRITE_CONTACTS
adb shell pm grant net.dinglisch.android.taskerm android.permission.CALL_PHONE
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_CALENDAR
adb shell pm grant net.dinglisch.android.taskerm android.permission.WRITE_CALENDAR
adb shell pm grant net.dinglisch.android.taskerm android.permission.CHANGE_CONFIGURATION
adb shell pm grant net.dinglisch.android.taskerm android.permission.ANSWER_PHONE_CALLS
adb shell pm grant net.dinglisch.android.taskerm android.permission.SET_MEDIA_KEY_LISTENER
adb shell pm grant net.dinglisch.android.taskerm android.permission.SYSTEM_ALERT_WINDOW
adb shell pm grant net.dinglisch.android.taskerm android.permission.SET_PROCESS_LIMIT
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_EXTERNAL_STORAGE
adb shell pm grant net.dinglisch.android.taskerm android.permission.ACCESS_BACKGROUND_LOCATION
```

#### 安装Tasker时获取

可以通过 (把Tasker安装文件放置到手机存储根目录)

```
adb shell pm install -g /storage/0/tasker.apk
```

或者(把Tasker安装文件放置到adb根目录)

```
adb install -g tasker.apk
```

这两种adb安装方式直接获取常规权限.

#### 安装Tasker后手动设置

可以在系统设置的应用管理界面手动赋予权限.

### 获取特殊权限的方法

特殊权限只能通过adb或者root授权:

```
adb shell pm grant net.dinglisch.android.taskerm android.permission.WRITE_SECURE_SETTINGS
adb shell pm grant net.dinglisch.android.taskerm android.permission.DUMP
adb shell pm grant net.dinglisch.android.taskerm android.permission.READ_LOGS
adb shell pm grant net.dinglisch.android.taskerm android.permission.SET_VOLUME_KEY_LONG_PRESS_LISTENER
adb shell pm grant net.dinglisch.android.taskerm android.permission.SET_MEDIA_KEY_LISTENER
```

截屏权限

```
adb shell appops set net.dinglisch.android.taskerm PROJECT_MEDIA allow
```

### Tasker需要开启的服务

无障碍服务(辅助功能) 和 通知管理服务,既可以手动通过系统设置赋权也可以使用下面的adb 命令开启

```
adb shell settings put secure enabled_accessibility_services net.dinglisch.android.taskerm/.MyAccessibilityService
adb shell settings put secure accessibility_enabled 1

adb shell settings put secure enabled_notification_listeners net.dinglisch.android.taskerm/.NotificationListenerService
adb shell settings put secure notification_enabled 1
```

开关移动数据需要 ADB over TCP 服务

```
adb tcpip 5555
```

设备拥有者，这个服务建议在新手机或者刷机的时候就设置，因为需要提前将手机上的所有账户都取消掉（甚至可能需要恢复工厂模式才行）

```
adb shell dpm set-device-owner net.dinglisch.android.taskerm/.MyDeviceAdminReceiver
```

![设备管理器][1] 
![辅助应用][2]
![辅助应用][3]
![通知使用权][4]
![电池优化][5]
![应用启动管理][6]

除此以外已知的还有 通知使用权,电池优化,应用自启,允许第三方启动,开机启动,助手设置 需要手动开启.

### 需要关闭的权限或者服务

#### 有些服务不关闭的话，会影响到Tasker的使用

涉及到短信的配置,建议关闭系统的短信验证码保护(例如:EMUI)

#### Tasker的bug造成系统出错

Android 10,Tasker 5.9.1 暂不建议开启 WRITE\_SECURE\_SETTINGS ,开启此权限可能会造成输入法被切换为Tasker，但是不开启可能会造成Tasker无法读取剪切板，可以使用下面的命令取消权限

```
adb shell pm revoke net.dinglisch.android.taskerm android.permission.WRITE_SECURE_SETTINGS
```

最后，如果你安装的是测试版，想要降回稳定版则可以使用下面的命令

```
adb install -r -d tasker.apk
```

注:基于Android 10,Tasker 5.9.1 不同系统版本和应用版本可能略有不同.


更新于 20210415


[1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E8%AE%BE%E5%A4%87%E7%AE%A1%E7%90%86%E5%99%A8.jpg
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E8%BE%85%E5%8A%A9%E5%BA%94%E7%94%A8a.jpg
[3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E8%BE%85%E5%8A%A9%E5%BA%94%E7%94%A8b.jpg
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E9%80%9A%E7%9F%A5%E4%BD%BF%E7%94%A8%E6%9D%83.jpg
[5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E7%94%B5%E6%B1%A0%E4%BC%98%E5%8C%96.jpg
[6]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/01/%E5%BA%94%E7%94%A8%E5%90%AF%E5%8A%A8%E7%AE%A1%E7%90%86.jpg
