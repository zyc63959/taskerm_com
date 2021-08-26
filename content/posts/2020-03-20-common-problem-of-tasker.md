---
title: Tasker常见问题解答
author: 记忆水晶
type: post
date: 2020-03-20T01:14:23+00:00
url: /2020/03/20/common-problem-of-tasker.html
views:
  - 370
categories:
  - 教程

---
**本篇文章不涉及到 HOW TO**

## 问题及解决方法

  1. 手机下拉通知栏提示”无活动的配置文件”
      * 原因:没有状态类的配置触发,都会有此提示.
      * 解决:该提醒可以忽略(通常安装Tasker第一天的小白,都会有这个疑问).
  2. 添加桌面小部件时提示”数据被阻止,请返回主应用,并在主界面上退出”
      * 原因:这种是Tasker的配置在修改后没有被保存,才会出现的提示.
      * 解决:一般在Tasker主界面的右上菜单中选中”退出”即可正常添加桌面小部件.
  3. Tasker导入配置文件时提示”对不起,Tasker无法处理该内容”
      * 原因:很可能是Tasker配置和Tasker版本不对应导致的
      * 解决:
          * 如果是通过配置文件导入,可以用文本编辑器打开,查看Tasker版本号,然后安装该版本的Tasker即可导入配置
          * 如果是通过配置链接导入,可以查看配置的分享日期,查询该日期相对应的Tasker版本(稳定版或测试版)
  4. Tasker导入prf.xml格式的文件时提示”错误:导入的内容中包含多个配置文件.”
      * 原因:可能是认为将工程文件prj.xml改为了prf.xml
      * 解决:将文件中的prf.xml改为prj.xml,按照工程文件的导入方式导入Tasker
  5. Tasker频繁提示”需要认证”，”点击此处认证Tasker”
      * 原因:Tasker新版强化了验证机制，Tasker的备份，配置导入导出等等行为都会验证是否正版
      * 解决:
          * 可以在系统设置的通知管理界面单独关闭Tasker的验证提醒
          * 换一个比较给力的上网工具