---
title: 用Tasker实现Android手机短信转发到钉钉
author: 记忆水晶
type: post
date: 2019-04-06T09:15:00+00:00
url: /2019/04/06/forwarded-sms-to-dingtalk.html
views:
  - 227
wpcom_likes:
  - 6
categories:
  - 教程
tags:
  - Tasker
  - 短信
  - 转发
  - 钉钉

---


        之前的一篇文章[《用Tasker实现Android手机短信转发到微信》](https://taskerm.com/2018/12/22/forwarded-sms-to-wechat.html)介绍了用tasker实现手机短信转发的功能，主要是介绍转发到微信的方法，对转发到钉钉的方法没有提及，前段时间有人在群里问了遇到了些问题，这里写个关于发送到钉钉教程。


 短信转发到钉钉上是使用的[企业版钉钉][1]的功能，企业钉钉有着丰富的可开发性。

 整个操作步骤是：1，注册企业钉钉；2，创建一个应用；3，在tasker中创建配置文件。

  1. 注册企业钉钉

  * a. 点击这里注册：<https://oa.dingtalk.com/> 1分钟时间注册下就行，比较简单。

  1. 创建一个企业内部应用

  * a.点击这里创建 <https://open-dev.dingtalk.com/#/create-app>

上传一个应用logo和自定义应用名字，应用类型为企业内部自主开发,其他默认。  
配置应用信息中的开发模式设置为开发应用,开发应用类型为微应用,其他服务器出口填写你的本机IP,其他随便填写.

  * b.创建后打开：<https://oa.dingtalk.com/index.htm#/microApp/microAppList>  
    可以看到在 &#8220;应用管理&#8221;中的&#8221;自建应用&#8221;里有个应用。
  * c.<https://open-dev.dingtalk.com/#/suite>

点进去打开可以看到微应用下面有个微应用管理。

  * d.右侧是创建的应用列表,点击创建的应用最右侧的设置,然后打开应用信息的基础信息
  * e.记录下来 **AgentId ,AppKey ,AppSecret** 这3个值备用。

  1. 创建tasker配置文件

下面是创建图示的说明

![点击加号--新建配置][2] 

![选择触发类型--事件][3] 

![选择触发条件类型--电话][4] 

![选择触发内容--收到短信][5] 

![点击返回][6] 

![新建任务][7] 

![自定义任务名字(可省略不填)][8] 

![点击名字右边的对号][9] 

![点击加号--新建操作][10] 

![选择代码][11] 

![选择JavaScriptlet][12] 

![在此位置填写代码][13] 

![假设填写 flash--好吧,截图截早了][14] 

![点击箭头--返回][15] 

![点击对号--保存][16] 

![这个是完成后看起来的样子][17] 

    //下面的三个变量值需要修改
    var AgentId = "200374588";
    var AppKey = "dingaaolalasl7feqdfg";
    var AppSecret = "abcedfg_abcedfgabcedfgabcedfgabcedfgabcedfg";
    
    //定义post方法
    function posthttp(url, data) {
        var xhr = new XMLHttpRequest();
        xhr.addEventListener("readystatechange", function () {
            if (this.readyState === 4) {
                flash(this.responseText); //显示返回消息,可删除本行
            }
        });
        xhr.open("POST", url, false);
        xhr.send(data);
        return xhr.responseText;
    }
    
    //定义get方法
    function gethttp(url) {
        var xhr = new XMLHttpRequest();
        xhr.addEventListener("readystatechange", function () {
            if (this.readyState === 4) {
                flash(this.responseText); //显示返回消息,可删除本行
            }
        });
        xhr.open("GET", url, false);
        xhr.send();
        return xhr.responseText;
    }
    
    //获取token
    var gettoken = "https://oapi.dingtalk.com/gettoken?appkey=" + key + "&appsecret=" + secret;
    var ACCESS_TOKEN = JSON.parse(gethttp(gettoken)).access_token;
    
    //发送消息(文本)
    var SMSRF = global('SMSRF');
    var SMSRB = global('SMSRB');
    var SMSRT = global('SMSRT');
    var SMSRD = global('SMSRD');
    var CONTENT = "发件人: " + SMSRF + "\n时间: " + SMSRT + ",  日期: " + SMSRD + "\n短信内容: " + SMSRB;
    var message = JSON.stringify({
        "touser": "@all",
        "msgtype": "text",
        "agent_id": agentId,
        "msg": {
            "msgtype":"text"
             "text":{
                  "content": CONTENT
          }
        },
    });
    var send = "https://oapi.dingtalk.com/topapi/message/corpconversation/asyncsend_v2?access_token=" + ACCESS_TOKEN;
    posthttp(send, message);

![在钉钉中收到的短信内容图示][18] 

**发送图片到钉钉的配置也完成了**

> 原文链接： [用Tasker实现Android手机短信转发到钉钉][19]

附上配置导入链接：

  * [点击我导入配置][20](需要tasker5.3以上的版本)
  * [点击我导入配置][21](需要tasker5.3以上的版本)

[点击我加入群【Tasker配置分享群】][22]

[1]: https://oa.dingtalk.com
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/0-1554532930.jpeg!large "点击加号--新建配置"
[3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/0-1554532931.jpeg!large "选择触发类型--事件"
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554532931.jpeg!large "选择触发条件类型--电话"
[5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554532932.jpeg!large "选择触发内容--收到短信"
[6]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/1-1554532933.jpeg!large "点击返回"
[7]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/10-1554532934.jpeg!large "新建任务"
[8]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/10-1554532935.jpeg!large "自定义任务名字(可省略不填)"
[9]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/8-1554532936.jpeg!large "点击名字右边的对号"
[10]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/10-1554532937.jpeg!large "点击加号--新建操作"
[11]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/10-1554532938.jpeg!large "选择代码"
[12]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554532939.jpeg!large "选择JavaScriptlet"
[13]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554532940.jpeg!large "在此位置填写代码"
[14]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/4-1554532941.jpeg!large "假设填写 flash--好吧,截图截早了"
[15]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/3-1554532942.jpeg!large "点击箭头--返回"
[16]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/4-1554532943.jpeg!large "点击对号--保存"
[17]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/04/9-1554532944.jpeg!large "这个是完成后看起来的样子"
[18]: https://upload-images.jianshu.io/upload_images/2483366-b89124f3694c9181.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240 "在钉钉中收到的短信内容图示"
[19]: https://taskerm.com/2019/04/06/forwarded-sms-to-dingtalk.html
[20]: https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw%2BJP1fYIWaL6G53enhFTrMP6xMnJawIbufv%2Fcr1krqlca25FgFK7KKdWs%3D&id=Profile%3A%E8%BD%AC%E5%8F%91%E7%9F%AD%E4%BF%A1%E5%88%B0%E5%BE%AE%E4%BF%A1
[21]: taskerprofile://H4sIAAAAAAAAAOVWX2/bVBR/bj6F5QfmaCHXcf60axyPpg3bWNdOjYWGhDTd2jeJtcR27Zu0BVVqJWCthogmjXaMwhgaPKDRIYFKW2D9MrHbfAvuHzv1yoDxjF/uved3zvE5v3Ouj1Ud+neQNwMxFHyvIoqC2bMqYk4UcK8iFrMlUUuNqTc9p2G1EdNwyT43MS4KPVQRFQqPqYYJMdJyxUJpIp+/lJPzuUsq4EIKo5dgJV8qKSpAI9gyNeJQBWSlx45lykRQUgHbUZHdQdrpH8+C/v2Txz8Ojp8Emz8FL/bIRgUUoir1FvR4gGzH4hpTTW3KNj3HMsOte+HuEbfmnhI+TK6MNRVg5gwwH2xb6yEbM7+GY8vJrEnajok0EjhbmcT1LE1WAV3Y+VpkC70mtYXtiiiLgGN17MVYjvvNvwJSXoJUwOKhNQFRUeieFpEZYLIh1J2rSrEwUVKKcl75z1UpjapCef4b+uIS0KxLo+TVKQNbjs3zMHBE3XiSuhwLaEReIms5zloDYHBwb/jVtyePPhocbA0Ofgj6D4d3+8H678Pd9dPvNwbHe+GDw1QPesK1GaEiiMvLeaM0jpBSmDDQ+PgiNMUyg+u16YWaTlWuzzWri62rlu4UCu8q+Q+WZnty771paN6qyaRd7KJTyBmdblVxCpHt1JXanM7952T6KARIARDsPRocbrmOj8Ptw/Dnz1ONrs3TprIWxq7U9doZgbAK08KHKYE81N9KyyO+bLQs3Loxe5WoLaClLvKxlC4zHYJnoWmyYs9aPkY28iTRQ9Bc9TGpkNGCdhOJGWH0Pil2Tx+rIUi4ZflZZlGnFkKlUhEKSSX6NNrQb8WqvuvYPtLRCk6XBQDChy9Onh6dHj8Ivvw63N8MN55ngv7zYPOb4RdPw91np08+HblaY7u1RPCOi2xJvDlf10mQjIIGbPsooeEj25QYL1zmIdz1bAYlQymn1s6IbqK/8ExEMc3/Q4Kv1P6Z39fi9vSzX4P+NnbuIJs1O6GUHWi3U279SQCWVqFrZZeRtWLZ2aWlrOF0gNG03ly0bBDrXzYcz7XMiihcpHfxoiC+ATtumUp9ZJAYGMKvYXStpqdr9fptff56bY687Z36/FzWhZ6PpLisse90OgsNA/n+bXbkl69/f7i+wZmTwu27hLM0v+k36gtvE3/NtrMI29IFdr6QLo/A6jmwmgT1c6CeBGfOgTMxOD0/p5NvBOWMxDX4bX9wdDQpsIRZNISN9+1wZ3+488uZWKfijCCEO9+Fu4/P5DNcPRp2n3wc7B2egVX+wg4hAzZRTJuPPctuWo1ViTegiJ2ujzyR2L0F220xw6Udv4lXXUTFmHRALCaObGyZRBx96SI505lM9DSdguSyUGGUMe/MSN+HDepbTq1FtNAufN0+ijIC1OZystqsb5K9Uk6NPq9UOROTkS6T0Y29f52vibGsRGM59wosH2GFYjx9+Uxj45fOXC3FV/4DpaX+BDlCtFBOCQAA
[22]: https://jq.qq.com/?_wv=1027&k=5rRyYlb