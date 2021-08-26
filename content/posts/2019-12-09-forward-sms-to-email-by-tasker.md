---
title: 使用Tasker实现短信转发到邮箱
author: 记忆水晶
type: post
date: 2019-12-09T21:12:00+00:00
url: /2019/12/09/forward-sms-to-email-by-tasker.html
views:
  - 211
categories:
  - 教程
tags:
  - email
  - forward
  - sms
  - 邮箱

---


## 引语

发送短信到邮箱的原理与[短信转发到微信](http://taskerm.com/2018/12/22/forwarded-sms-to-wechat)有些类似.

## 原理

  发送短信到邮箱是利用Ifttt这个服务将短信转发到邮箱中.Ifttt服务的可扩展性很强.

## 步骤

  1.注册Ifttt,2.创建一个Applet,3.在tasker中创建配置文件

1. 注册[Ifttt](https://ifttt.com/user/new?wp_=1).
2. 创建一个[Applet](https://ifttt.com/create) 
	* a. this 选择 [webhooks](https://ifttt.com/maker_webhooks),并设定一个**_event_**名字
	* b. that 选择 [email](https://ifttt.com/email) 
	* c. 打开[webhooks服务设置](https://ifttt.com/maker_webhooks/settings)记录下URL中的最后一个”/”后的字符串(也就是_**key**_) 
3. 在Tasker中创建配置

    详细步骤不再赘述,不知道如何操作的可移步这里<a target="_blank" rel="noreferrer noopener">用Tasker实现短信转发到微信</a>;以`接收到的短信`为触发条件,创建任务添加操作`JavaScriptlet`后,代码处填写如下内容:


```
//下面的两个变量值需要修改 
var key = "cKKMTg7MnZKqQPFnJK__3N";//这个是你的ifttt提供的key 
var event = "短信转发到邮箱";//这个是你自己设定的Applet名字 
//定义post方法 
function postHttp(url, data) { 
  var xhr = new XMLHttpRequest(); 
  xhr.addEventListener("readystatechange", function() { 
    if (this.readyState === 4) { 
      //flash(this.responseText); 
      //显示返回消息,可删除本行 
    } 
  }); 
  xhr.open("POST", url, false); 
  xhr.setRequestHeader("Content-Type", "application/json"); 
  xhr.send(data); 
  return xhr.responseText; 
} 
//获取消息 
var smsrf = global("SMSRF"); 
var smsrb = global("SMSRB").replace(/[\n\r]/g, "&lt;br&gt;"); 
var mmsrs = global("MMSRS"); 
var smsrt = global("SMSRT").replace(/./, ":"); 
var smsrd = global("SMSRD"); 
//判断是短信,彩信还是无法获取短信内容 
smsrb = 
  smsrb == "%SMSRB" ? (mmsrs == "%MMSRS" ? "无法获取短信内容" : mmsrs) : smsrb; 
if (smsrb == "无法获取内容") { 
  flashLong(smsrb); 
} else { 
  var url = "https://maker.ifttt.com/trigger/" + event + "/with/key/" + key; 
  var value1 = "value1", 
    value2 = "value2", 
    value3 = "value3"; 
  var data = JSON.stringify({ 
    value1: smsrf, 
    value2: smsrt + " " + smsrd, 
    value3: smsrb 
  }); 
  var ifttt_text = unescape(postHttp(url, data)); 
  var text = "Congratulations! You've fired the " + event + " event"; 
  if (ifttt_text) { 
    if (ifttt_text == text) { 
      flash("短信发送成功"); 
    } else { 
      flashLong("短信发送失败"); 
    } 
  } else { 
    flash("短信发送失败,请检查网络"); 
  } 
} 
```

最后保存配置,这样就实现了短信转发到邮箱的功能.

## 视频演示

## 此方法的优点：

  1. 稳定  

    虽然之前的教程都是单独用Tasker或者单独用Ifttt来实现,不过实际操作下来感觉要么难以入手,要么不稳定.使用Tasker+Ifttt结合的方法比较稳定可靠.
  2. 可链接的服务多  

    得益于Ifttt的互联网属性,除了用此方法实现发送短信到邮箱,亦可将短信转发到telegram,google keep,google calendar,trello,Evernote等等服务中
  3. 正常上网即可实现，无需特殊联网  

    Ifttt在国内可正常使用，仅需在账户绑定的时候需要特殊网络环境
  4. 可自定义程度高  

    可以实现将特定特征的短信发送到一个服务中,将具有另一种特征的短信转发到另一个服务中而不冲突.

  


  如果你是第一天使用Tasker请看下本站的&nbsp;<a rel="noreferrer noopener" href="http://taskerm.com/2019/05/03/what-to-do-after-install-tasker/" target="_blank">Tasker安装第一天的教程</a>.

最后附上Tasker配置连接:<a href="https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw+JP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs=&id=Profile:%E8%BD%AC%E5%8F%91%E7%9F%AD%E4%BF%A1%E5%88%B0%E9%82%AE%E7%AE%B1" target="_blank" rel="noreferrer noopener">https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw+JP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs=&id=Profile:转发短信到邮箱</a>&nbsp;新增标签