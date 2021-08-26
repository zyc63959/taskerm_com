---
title: 用Tasker实现收到Android手机短信自动转发到微信
author: 记忆水晶
type: post
date: 2018-12-22T03:46:55+00:00
url: /2018/12/22/forwarded-sms-to-wechat.html
views:
  - 629
categories:
  - 配置

---
前言
--

之前的一篇文章[《用Tasker实现Android手机短信转发到Telegram》](http://taskerm.com/2018/02/08/forward-sms-to-telegram)介绍了用tasker实现手机短信转发的功能，主要是介绍转发到Telegram的方法，对转发到微信的方法一句带过，鉴于某些原因没有详细介绍，本篇简单介绍下如何使用tasker自动转发手机短信到微信上。

原理
--

短信转发到微信上是使用的[企业微信](https://work.weixin.qq.com/)的一项功能：企业微信收到的信息可以同步到微信，而企业微信有着丰富的可开发性。

步骤
--

整个操作步骤是：1.注册企业微信；2.创建一个应用；3.在tasker中创建配置文件。

### 注册企业微信

* a. 点击这里注册：[https://work.weixin.qq.com/wework\_admin/register\_wx?from=myhome](https://work.weixin.qq.com/wework_admin/register_wx?from=myhome) 1分钟时间注册下就行，比较简单。
* b. 注册完成后打开：[https://work.weixin.qq.com/wework_admin/frame#profile](https://work.weixin.qq.com/wework_admin/frame#profile) **复制下网页底部的企业信息中的企业ID备用**。
* c. 点击[微工作台https://work.weixin.qq.com/wework_admin/frame#profile/wxPlugin](https://work.weixin.qq.com/wework_admin/frame#profile/wxPlugin)看到一个二维码,使用微信扫码关注,这样就可以**使企业微信中收到的信息同步到微信上**。

### 创建一个应用

* a.点击这里创建 [https://work.weixin.qq.com/wework_admin/frame#apps/createApiApp](https://work.weixin.qq.com/wework_admin/frame#apps/createApiApp)  
    上传一个应用logo和自定义应用名字，其他默认。
* b.创建后打开：[https://work.weixin.qq.com/wework_admin/frame#apps](https://work.weixin.qq.com/wework_admin/frame#apps) 可以看到在 “应用”中的“自建”里有个应用。点进去打开**记录下 AgentId和Secret备用**。

### 创建tasker配置文件

    下面是创建图示的说明

![此图像的alt属性为空；文件名为5-1554217206.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/5-1554217206.jpeg!default)

点击加号–新建配置

![此图像的alt属性为空；文件名为6-1554217207.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/6-1554217207.jpeg!default)

选择触发类型–事件

![此图像的alt属性为空；文件名为9-1554217210.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554217210.jpeg!default)

选择触发条件类型–电话

![此图像的alt属性为空；文件名为6-1554217211.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/6-1554217211.jpeg!default)

选择触发内容–收到短信

![此图像的alt属性为空；文件名为6-1554217212.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/6-1554217212.jpeg!default)

点击返回

![此图像的alt属性为空；文件名为1-1554217215.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554217215.jpeg!default)

新建任务

![此图像的alt属性为空；文件名为2-1554217216.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/2-1554217216.jpeg!default)

自定义任务名字(可省略不填)

![此图像的alt属性为空；文件名为6-1554217217.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/6-1554217217.jpeg!default)

点击名字右边的对号

![此图像的alt属性为空；文件名为3-1554217218.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/3-1554217218.jpeg!default)

点击加号–新建操作

![此图像的alt属性为空；文件名为9-1554217219.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554217219.jpeg!default)

选择代码

![此图像的alt属性为空；文件名为2-1554217220.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/2-1554217220.jpeg!default)

选择JavaScriptlet

![此图像的alt属性为空；文件名为1-1554217221.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554217221.jpeg!default)

在此位置填写代码

![此图像的alt属性为空；文件名为5-1554217223.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/5-1554217223.jpeg!default)

假设填写 flash–好吧,截图截早了，把图中的flash改为文章底部的代码

![此图像的alt属性为空；文件名为0-1554217227.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/0-1554217227.jpeg!default)

点击箭头–返回

![此图像的alt属性为空；文件名为1-1554217228.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554217228.jpeg!default)

点击对号–保存

![此图像的alt属性为空；文件名为3-1554217229.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/3-1554217229.jpeg!default)

这个是完成后看起来的样子

```javascript
//下面的三个变量值需要修改  
var ID = "ww3c067de248ce7eb1ad";  
var SECRET = "KNgBbhHiTo55VSVzqLv0vYCadXE0ndrn5o41cmuB2o4";  
var AGENTID = 1000002;  
//获取消息  
var smsrf = global('SMSRF');  
var smsrb = global('SMSRB');  
var mmsrs = global('MMSRS');  
var smsrt = global('SMSRT').replace(/\./, ":");  
//flash(smsrf)  
var pnum = global('PNUM').substring(3)||"未知的号码";  
var smsrd = global('SMSRD');  
//定义post方法  
function postHttp(url, data)  
{  
var xhr = new XMLHttpRequest();  
xhr.addEventListener("readystatechange", function ()  
{  
if (this.readyState === 4) {  
flash(this.responseText);  
//显示返回消息,可删除本行  
}  
});  
xhr.open("POST", url, false);  
xhr.send(data);  
return xhr.responseText;  
}  
//定义get方法  
function getHttp(url)  
{  
var xhr = new XMLHttpRequest();  
xhr.addEventListener("readystatechange", function ()  
{  
if (this.readyState === 4) {  
flash(this.responseText);  
//显示返回消息,可删除本行  
}  
});  
xhr.open("GET", url, false);  
xhr.send();  
return xhr.responseText;  
}  
//判断是短信,彩信还是无法获取短信内容  
smsrb = (smsrb == "%SMSRB") ? (mmsrs == "%MMSRS") ? "无法获取短信内容" : mmsrs : smsrb;  
//  
if (smsrb == "无法获取内容") {  
flashLong(smsrb)  
}  
else  
{  
//获取token  
var tokenUrl = "https://qyapi.weixin.qq.com/cgi-bin/gettoken?corpid=" + ID + "&corpsecret=" + SECRET;  
var access_tokenJson = JSON.parse(getHttp(tokenUrl));  
if (access_tokenJson.errcode == 0)  
{  
var access_token = access_tokenJson.access_token;  
//发送消息(文本)  
var content = "发件人: " + smsrf + "\n收件人: " + pnum + "\n时间: " + smsrt + ", 日期: " + smsrd + "\n短信内容: " + smsrb;  
var message = JSON.stringify(  
{  
"touser" : "@all", //@all代表发送给全体成员，也可指定某几个人,比如"a|b|c"  
//"toparty" : "1|2",//部门id  
//"totag" : "1|2",//标签id,文档说明：https://work.weixin.qq.com/api/doc#90000/90135/90236  
"msgtype" : "text", "agentid" : AGENTID, "text" : {  
"content" : content  
},  
"safe" : 0  
});  
var msgUrl = "https://qyapi.weixin.qq.com/cgi-bin/message/send?access_token=" + access_token;  
postHttp(msgUrl, message)  
}  
else if (access_tokenJson.errcode == 40013) {  
flashLong("ID 错误,请检查是否修改正确(请注意不要有空格)");  
}  
else if (access_tokenJson.errcode == 40001) {  
flashLong("SECRET 错误,请检查是否修改正确(请注意不要有空格)");  
}  
};
```


![此图像的alt属性为空；文件名为3-1554217230.jpeg!default](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/3-1554217230.jpeg!default)

在微信中收到的短信内容图示

**发送图片到微信的配置也完成了**

配置链接
----

附上配置导入链接：

* [点击我导入配置](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv%2Fcr1krqlca25FgFK7KKdWs%3D&id=Profile%3A%E8%BD%AC%E5%8F%91%E7%9F%AD%E4%BF%A1%E5%88%B0%E5%BE%AE%E4%BF%A1)(需要tasker5.3以上的版本)

注意事项
----

1.  华为手机需要关闭短信验证码保护功能，否则含有验证码的短信无法读取。
2.  小米手机可能需要打开短信通知。
3.  已知华为、小米、一加、三星、OPPO、vivo等机型可用； 360、坚果、魅族部分机型无法使用。
4.  如果不打开企业微信信息同步到微信的开关的话，微信时收不到信息的。

> 更新于 20210805
