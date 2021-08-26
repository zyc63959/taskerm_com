---
title: Tasker填坑指南
author: 记忆水晶
type: post
date: 2020-12-04T11:50:00+00:00
url: /2020/12/04/how-to-use-tasker-app.html
views:
  - 408
categories:
  - 教程
tags:
  - 教程

---
## Tasker的坑还是蛮多的

* Tasker提示试用到期，需要付费使用
  好吧，这个是为国内无法付费使用的设备设置的。
    
  首先需要说明的是Tasker是付费应用，收到这个提示是正常的。但是在Android手表，Android车机等设备使用则需要绕过这个提示，否则无法使用。这里给出一个绕过该提示的方法：首先确定设备上是否有Android套件，如果手机上安装有 Google play 框架，首先卸载掉，并安装一个play商店应用，最后安装最新正版的Tasker，这样Tasker就不会再提示付费使用了。</li> 
    
* Tasker总是被优化掉
  
  需要设置三项内容即可解决，具体可在[Tasker安装第一天的教程][1]中找到
  
    * 添加Tasker到电池优化白名单
    * 在应用启动管理中选择手动启动：依次开启：自启动、关联启动、后台活动
    * 在最近任务中锁定Tasker应用
* 无法被卸载
  这个是因为开启Tasker设备管理器，在系统管理器中取消Tasker就行</li> 
  
* 辅助功能总是掉
这个应该是第一个问题的附带影响，通常解决问题2即可解决；但是手机如果经常关机的话，可能也会造成辅助功能经常被关闭，这时可以使用 自动开启Tasker的辅助功能 这个配置来解决</li> 

* 权限已经给全，仍提示无权限

  * 这个应该可能是应用bug的锅，我最近不怎么遇到了，应该是最新版解决了该问题，不过如果遇到了，可以临时把权限关闭了重新打开试试
  * 另外也可能是提示错误造成的，如果上个解决方法不行，可以参考这里[一次性给出所有的权限][2]，不过这个页面提到的权限并不一定完整，随着Tasker更新，所需要的权限会更全面。
* 插件或者第三方应用无法被调用
这个问题的原因我已经说过了，解决方法也提到了，大家可自行解决。如果懒得弄，可以直接[导入这个配置][3]</li> </ol> 

## Tasker问题反馈

如果你遇到无法解决的问题，可以在reddit 或者 Google group 反馈问题，作者回复很及时。当然也可以在百度贴吧上提问。

> 问题1的解决方法是大佬 273.15 提供的，你可以在csdn或酷安找到他。

 [1]: https://taskerm.com/2019/05/03/what-to-do-after-install-tasker.html
 [2]: https://taskerm.com/2020/01/31/how-to-enable-all-permissions-and-services-required-by-tasker-in-pc.html
 [3]: https://pan.baidu.com/s/1VJxBcV7Auauf5d7iiJc1CA