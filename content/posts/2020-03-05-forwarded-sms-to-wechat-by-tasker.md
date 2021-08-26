---
title: 在Tasker中利用短信的通知实现短信内容转发到微信
author: 记忆水晶
type: post
date: 2020-03-05T09:59:00+00:00
url: /2020/03/05/forwarded-sms-to-wechat-by-tasker.html
featured_image: /wp-content/uploads/2020/03/新建配置-480x300.jpg
views:
  - 400
categories:
  - 教程
tags:
  - JavaScript
  - 实例
  - 微信
  - 脚本
  - 转发

---
之前的教程是利用Tasker自带的短信变量来实现的，这有一个无法解决问题：在360，魅族，坚果等品牌的手机中无法获取短信的消息内容。
利用短信的通知则可以获取短信的内容，并且对于 华为手机 来说也可以不用关闭短信验证码保护功能，所以相较于原来的方法更简单，方便。
应用通知的变量是一个本地数组变量 %evtprm() ,这个变量数组包含 %evtprm1，%evtprm2等本地变量，其中%evtprm2含有发件人信息，%evtprm3含有通知的具体消息内容。

操作步骤：1，注册企业微信；2，创建一个应用；3，在tasker中创建配置文件。

1. 注册企业微信
- a. 点击这里注册：[https://work.weixin.qq.com/wework_admin/register_wx?from=myhome](https://work.weixin.qq.com/wework_admin/frame#profile)  1分钟时间注册下就行，比较简单。
- b. 注册完成后打开：[https://work.weixin.qq.com/wework_admin/frame#profile](https://work.weixin.qq.com/wework_admin/frame#profile) **复制下网页底部的企业信息中的企业ID备用**。
- c. 点击[微工作台https://work.weixin.qq.com/wework_admin/frame#profile/wxPlugin](https://work.weixin.qq.com/wework_admin/frame#profile/wxPlugin)看到一个二维码,使用微信扫码关注,这样就可以**使企业微信中收到的信息同步到微信上**。
2. 创建一个应用
- a.点击这里创建 [https://work.weixin.qq.com/wework_admin/frame#apps/createApiApp](https://work.weixin.qq.com/wework_admin/frame#apps/createApiApp)
上传一个应用logo和自定义应用名字，其他默认。
- b.创建后打开：[https://work.weixin.qq.com/wework_admin/frame#apps](https://work.weixin.qq.com/wework_admin/frame#apps) 可以看到在 "应用"中的"自建"里有个应用。点进去打开**记录下 AgentId和Secret备用**。
3. 创建tasker配置文件
下面是创建图示的说明

![点击加号--新建配置](https://oss.taskerm.com/2020/03/新建配置.jpg!watermark "新建配置")

![选择触发类型--事件](https://oss.taskerm.com/2020/03/事件.jpg!watermark "事件")

![选择触发条件类型--界面](https://oss.taskerm.com/2020/03/界面.jpg!watermark "界面")

![选择触发内容--通知](https://oss.taskerm.com/2020/03/通知.jpg!watermark8 "通知")
![选择短信应用--信息](https://oss.taskerm.com/2020/03/信息.jpg!watermark8 "信息")

![点击返回](https://oss.taskerm.com/2020/03/返回.jpg!watermark)

![新建任务](https://oss.taskerm.com/2020/03/新建任务.jpg!watermark)

![点击名字右边的对号](https://oss.taskerm.com/2020/03/对号.jpg!watermark)

![点击加号--添加操作](https://oss.taskerm.com/2020/03/添加操作.jpg!watermark "添加操作")

![选择代码](https://oss.taskerm.com/2020/03/代码.jpg!watermark "代码")

![选择JavaScriptlet](https://oss.taskerm.com/2020/03/JavaScriptlet.jpg!watermark "JavaScriptlet")

![在此位置填写文末代码](https://oss.taskerm.com/2020/03/填写代码.jpg!watermark)

![点击箭头--返回](https://oss.taskerm.com/2020/03/返回.jpg!watermark "返回")

![点击对号--保存](https://oss.taskerm.com/2020/03/保存.jpg!watermark "保存")

![这个是完成后看起来的样子](https://oss.taskerm.com/2020/03/完成后的图示.jpg!watermark "完成后的图示")

```javascript {.line-numbers}
//下面的三个变量值需要修改
var ID = "ww3c67de248cf7ebad";
var SECRET = "KngBbhHiT055VSVzqLv0vYCadXE0ndrn5o41cmuB2o4";
var AGENTID = 1000002;
//获取消息

var pnum = global('PNUM');
//定义post方法
function postHttp(url, data) 
{
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () 
    {
        if (this.readyState === 4) {
            //flash(this.responseText);
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
            //flash(this.responseText);
            //显示返回消息,可删除本行
        }
    });
    xhr.open("GET", url, false);
    xhr.send();
    return xhr.responseText;
}


    //获取token
    var tokenUrl = "https://qyapi.weixin.qq.com/cgi-bin/gettoken?corpid=" + ID + "&corpsecret=" + SECRET;
    var access_tokenJson = JSON.parse(getHttp(tokenUrl));
    if (access_tokenJson.errcode == 0)
    {
        var access_token = access_tokenJson.access_token;
        //发送消息(文本)
        var content = "发件人: " + evtprm[1] + "\n收件人: " + pnum + "\n短信内容: " + evtprm[2];
        var message = JSON.stringify(
        {
            "touser" : "@all", //@all代表发送给全体成员，也可指定某几个人,比如"a|b|c"
            //"toparty" : "1|2",//部门id
            //"totag" : "1|2",//标签id
            "msgtype" : "text", "agentid" : AGENTID, "text" : {
                "content" : content 
            },
            "safe" : 0
        });
        var msgUrl = "https://qyapi.weixin.qq.com/cgi-bin/message/send?access_token=" + access_token;
     postHttp(msgUrl, message) 
    }

```


![在微信中收到的短信内容图示](https://oss.taskerm.com/2020/03/在微信中收到的短信内容图示.jpg!watermark "在微信中收到的短信内容图示")

`注:1.为保证Tasker正常运行,请将Tasker加入电池白名单,即允许Tasker后台运行.允许Tasker自启.允许Tasker被第三方应用启动.`
`2.为保证配置正常触发,请将Tasker的通知使用权和通知管理权打开.`

> 基于Android 10 ，EMUI 系统测试