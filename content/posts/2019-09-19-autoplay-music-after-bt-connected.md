---
title: 蓝牙耳机与手机连接后自动播放手机本地音乐
author: 记忆水晶
type: post
date: 2019-09-19T09:39:00+00:00
url: /2019/09/19/autoplay-music-after-bt-connected.html
featured_image: /wp-content/uploads/2019/09/蓝牙耳机与手机连接后自动播放手机本地音乐-480x300.jpg
views:
  - 158
categories:
  - 教程

---
使用背景:连接车载蓝牙后播放音乐,连接蓝牙耳机蓝牙音箱播放本地音乐或者播客等等.

  1. 触发条件选择 状态&nbsp;`蓝牙已连接`
  2. 新建匿名任务 添加操作&nbsp;`媒体控制`
  3. 在媒体控制界面设置以下内容:

  * a.&nbsp;`Cmd`&nbsp;选为&nbsp;`Play`
  * b. 选中&nbsp;`模拟媒体按钮`
  * c. 点击&nbsp;`程序`&nbsp;右边的搜索按钮选择音乐应用
  * d. 选中&nbsp;`Use Notification If Available`<figure class="wp-block-image size-large">

![蓝牙耳机与手机连接后自动播放手机本地音乐][1] </figure> 


> 为了避免连接非蓝牙耳机音响等设备触发任务,可以在蓝牙已连接的界面选择名称或者MAC地址.


除此以外并不需要进行其他设置,即可正常运行,如果运行不正常可以参考&nbsp;[安装第一天的教程][2]

[1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/%E8%93%9D%E7%89%99%E8%80%B3%E6%9C%BA%E4%B8%8E%E6%89%8B%E6%9C%BA%E8%BF%9E%E6%8E%A5%E5%90%8E%E8%87%AA%E5%8A%A8%E6%92%AD%E6%94%BE%E6%89%8B%E6%9C%BA%E6%9C%AC%E5%9C%B0%E9%9F%B3%E4%B9%90.jpg
[2]: https://taskerm.com/2019/05/03/what-to-do-after-install-tasker/