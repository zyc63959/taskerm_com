---
title: Tasker 教程之 JavaScript—-Tasker 小白的进阶之路
author: 记忆水晶
type: post
date: 2020-04-10T03:13:40+00:00
url: /2020/04/10/tasker-javascript.html
featured_image: /wp-content/uploads/2020/04/js-节气-Google-search-result-480x300.png
views:
  - 261
wpcom_likes:
  - 1
categories:
  - 教程
tags:
  - JavaScript
  - Tasker
  - 脚本

---
**我们先用一个实例来演示如何利用JavaScript来创建一个配置**

## 配置实例

我打算创建一个这样的配置：根据当天是否是一个节气日来改变桌面壁纸，称之为节气壁纸配置，简称“节气壁纸”。  
但是我不懂得如何判断当天是否是一个节气日怎么办呢？答案是“搜索”。

### 搜索代码

通过搜索关键词“js 节气”得到如图所示的结果

![][1] 
js 节气 搜索结果

第一个搜索结果是获取公历农历节气的，因为不需要获取这么多的内容，放弃;打开第二个搜索结果，只有一个function，看着可以拿来使用，经测试的确可用。

### 修改代码

根据作者的注释，第一部分内容是判断当天是哪一个节气，第二部分是当天处于哪个节气日之后，所以把第二部分的内容删除，用第一部分代码。  
修改结果如图所示：

![][2]
![][3]
修改后的JS代码

这个方法用到三个参数，年月日，那么如何用变量来表示呢，这个也是可以搜索到的，首先搜索关键词“js 日期”，

![][4] 
JS日期搜索结果

点开第一条搜索结果

![][5] 
JavaScript Date 对象

找到“JavaScript Date 对象参考手册”

![][6] 
日期方法

，点击去就看到年月日的表示方法了，添加后的代码就像这样，

![][7] 
最后的代码

### 在Tasker添加操作

  1. 在Tasker的任务中添加代码操作JavaScriptlet将上面的代码复制粘贴进去就可以了
  2. 然后添加一个设置壁纸的操作(请自备24节气图片资源并以节气命名,并不需要与图中一致)![节气壁纸路径][8]节气壁纸路径

最后保存下配置就实现了这个功能。

为了避免路径出错，建议先选择一个壁纸，然后把路径中的节气改成变量。  
遇到逻辑方法的时候用JS，遇到Android功能实现的时候用Tasker自带功能。

### 添加触发条件

最后为这个任务添加一个&#8221;屏幕被解锁的触发条件&#8221;关联起来就完成。  
这样在不懂算法的情况下，也可以创建自己想要的配置了。

## 在Tasker中使用JavaScript解决逻辑问题

### 处理字符串

逻辑处理最经常遇到这样的提问，一个字符串 abcABC123F 怎么提取数字，这个时候直接搜索关键词 &#8220;js 提取数字&#8221; 就可以了

### 处理数据内容

用JavaScript处理HTML,XML,JSON等格式的数据也容易许多,比如解析一个简单的天气数据：像这样的`{"today":"雨"，"tomorrow":"晴"}`的JSON数据只需要使用`JSON.today`就解析完成了，非常简单。  
虽然像文首的例子可以网络获取到数据，但是解析数据还是用JavaScript方便，比Tasker内置的变量分离，搜索替换等功能方便很多。

## Tasker使用JavaScript的好处

  1. 入门低js语言足够成熟，学习资料丰富
  2. 运行速度快经实际测验，在Tasker中使用JavaScript处理复杂数据时，速度比Tasker内置功能快
  3. 可复用使用js代码时，直接复制粘贴原有代码就可以了，不必像Tasker内建功能那样，调用任务时还要设置参数
  4. 代码可以通过网络找到js代码搜索一下可以很方便找到，不仅仅可以在几个tasker群里面问了，完全可以到js群里问
  5. 兼容性好Tasker版本更替较快，导出的配置常常在不同版本间不兼容，使用js则可以大大减少不兼容现象的出现

## 建议

对于Tasker新人来说，并不强调所有的功能都使用JS来实现：遇到逻辑方法的时候用JS，遇到Android功能实现的时候用Tasker自带功能。  
如果你对tasker功能，运行日志，权限等都很熟悉，应该就成为tasker大神级别了吧！  
_当然，人人都能成为的大神不是真正的大神。_

## 展望

我并不是建议大家为了使用Tasker而从头学习JavaScript，只是推荐大家学会使用网上已有的代码，当然如果你因此而喜欢上js代码更好；写此篇文章的目的是：希望在未来5年，可以让更多的人上手Tasker，有更多的配置流行出来，让Tasker真正的为大多数人获得便利。

 [1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/js%20%E8%8A%82%E6%B0%94%20Google%20search%20result.png
 [2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/js%20%E8%8A%82%E6%B0%94%20code%20fixed.jpg
 [3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/js%20%E8%8A%82%E6%B0%94%20code.jpg
 [4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/js%20%E6%97%A5%E6%9C%9F%20Google%20search%20result.png
 [5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/data%E5%AF%B9%E8%B1%A1.png
 [6]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/%E8%8E%B7%E5%8F%96%E6%97%A5%E6%9C%9F%E7%9A%84%E6%96%B9%E6%B3%95.png
 [7]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/js%20%E8%8A%82%E6%B0%94.jpg
 [8]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2020/04/%E8%8A%82%E6%B0%94%E5%A3%81%E7%BA%B8%E8%B7%AF%E5%BE%84.jpg