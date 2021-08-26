---
title: Tasker安装第一天的教程
author: 记忆水晶
type: post
date: 2019-05-03T01:39:00+00:00
url: /2019/05/03/what-to-do-after-install-tasker.html
views:
  - 466
categories:
  - 教程

---
## 引言

第一次安装Tasker后发现,应用会在需要的时候主动引导用户获取相应的权限.  
此时根据提示操作一般不会引起意外的错误,如果不按照提示操作,可能会遇到茫然的错误.

## 新手需要做什么

  * 如果你是只想实现某一个或几个功能，那么找到可靠的配置文件或者配置链接([Tasker如何导入配置][1])，并且Tasker保持正常运行,应用进程不被系统优化掉(Tasker保活)就足够了。
  * 如果你想自己创建配置，实现更多的自定义功能，就需要一步一步按照如下步骤操作。

## 如何让Tasker保持正常运行

其实Tasker程序安装后打开应用，在Tasker主界面上，打开右上角的菜单，单击更多选项，点击Android设置，该界面一共罗列了10项设置，按照提示一步一步设置就可以了，并没有需要特别说明的地方。只是以下三点需要注意：

  1. 防止系统清理：进入系统最近任务界面，点击Tasker应用旁边的小锁，锁定Tasker不被系统清理
  2. 忽略电池优化：依次打开系统设置，应用和通知，应用管理，设置，特殊访问权限，忽略电池优化（直接在设置搜索栏搜索电池也能找到），允许忽略Tasker
  3. 设置启动管理：依次打开系统设置，电池，启动管理，关闭Tasker自动管理后弹出的对话框中选中：允许自启动，允许关联启动，允许后台活动  
![Tasker-防杀][2] 
  4. 最后，为Tasker赋予写安全权限。  

电脑上安装 adb后就可以使用以下命令获取权限

> 如何安装和使用adb请自行搜索

`adb shell pm grant net.dinglisch.android.taskerm android.permission.WRITE_SECURE_SETTINGS`


这个方法实现了很多需要root权限或者无障碍服务才能的功能:自动给自己添加辅助,打开通知管理权,改变系统的安全设置等等

其他还需要的权限可参考 [如何在PC端一次性开启Tasker的所有权限和服务][3]

## 其他技能

### 会查看运行日志

![Tasker安装第一天的教程][4] 

运行日志
    
### 配置自动备份 
![Tasker安装第一天的教程][5] 

备份

如果你是从低版本(5.2及之前的版本)升级的,最好在升级后备份下应用和应用数据,卸载,再全新安装Tasker,之后恢复应用数据.
        
## 注意
        
* Tasker权限和服务的设置虽然简单,但是如果不进行设置会造成各种意外的错误,浪费过多不必要的时间.
* 5.8前后的版本的配置互相冲突,可能造成无法导入的现象.参考 [Tasker常见问题解答][6]

[1]: https://taskerm.com/2019/10/12/tasker-basic-course/
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/10/%E5%90%AF%E5%8A%A8%E7%AE%A1%E7%90%86.jpg!default "Tasker-防杀"
[3]: https://taskerm.com/2020/01/31/how-to-enable-all-permissions-and-services-required-by-tasker-in-pc/
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/05/8-1557306031.jpeg!default "Tasker安装第一天的教程"
[5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/05/1-1557306034.jpeg!default "Tasker安装第一天的教程"
[6]: https://taskerm.com/2020/03/20/common-problem-of-tasker/