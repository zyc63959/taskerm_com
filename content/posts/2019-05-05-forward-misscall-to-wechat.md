---
title: 发送未接来电信息到微信
author: 记忆水晶
type: post
date: 2019-05-05T21:17:50+00:00
url: /2019/05/05/forward-misscall-to-wechat.html
featured_image: /wp-content/uploads/2019/05/0-1557191675-480x300.png
views:
  - 145
categories:
  - 教程
tags:
  - JavaScript
  - Tasker
  - 微信
  - 未接来电
  - 脚本
  - 转发

---
  之前做的《用Tasker实现Android手机短信转发到微信》,很多人询问如何发送未接来电信息,问的人太多就做出来.  
  本教程的大部分内容都跟《用Tasker实现Android手机短信转发到微信》的内容差不多少,只有发送信息的主体从短信改为未接来电,触发条件改成 未接来电 就可以了

##### 整个操作步骤是：1，注册企业微信；2，创建一个应用；3，在tasker中创建配置文件。

![发送未接来电信息到微信](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/05/0-1557191675.png "发送未接来电信息到微信")

![发送未接来电信息到微信](https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/05/0-1557191675.png "发送未接来电信息到微信")

实际效果截图
```javascript

//下面的三个变量值需要修改
var ID = "ww3c67de428ec7ebad";
var SECRET = "KNgBbbHiTo66VSVzqLv0vYCadXE11drn5o41cmuB2o4";
var AGENTID = 1000002;

//定义post方法
function postHttp(url, data) {
  var xhr = new XMLHttpRequest();
  xhr.addEventListener("readystatechange",
  function() {
    if (this.readyState === 4) {
      flash(this.responseText); //显示返回消息,可删除本行
    }
  });
  xhr.open("POST", url, false);
  xhr.send(data);
  return xhr.responseText;
}

//定义get方法
function getHttp(url) {
  var xhr = new XMLHttpRequest();
  xhr.addEventListener("readystatechange",
  function() {
    if (this.readyState === 4) {
      flash(this.responseText); //显示返回消息,可删除本行
    }
  });
  xhr.open("GET", url, false);
  xhr.send();
  return xhr.responseText;
}

//获取token
var tokenUrl = "https://qyapi.weixin.qq.com/cgi-bin/gettoken?corpid=" + ID + "&corpsecret=" + SECRET;
var access_token = JSON.parse(getHttp(tokenUrl)).access_token;

//发送消息(文本)
var cnum = global('CNUM');
cnum = cnum ? cnum: "来电未显示号码";
var cname = global('CNAME');
cname = (cname == "?") ? cnum: cname;
var ctime = global('CTIME').replace(/\./, ":");
var cdate = global('CDATE');

var content = "您有一条未接来电信息\n名字: " + cname + "\n号码: " + cnum + "\n时间: " + ctime + ",  日期: " + cdate;
var message = JSON.stringify({
  "touser": "@all", //@all代表发送给全体成员，也可指定某几个人,比如"hong|dan|tom"
  //"toparty" : "1|2",//部门id
  //"totag" : "1|2",//标签id,文档说明：https://work.weixin.qq.com/api/doc#90000/90135/90236
  "msgtype": "text",
  "agentid": AGENTID,
  "text": {
    "content": content
  },
  "safe": 0
});
var msgUrl = "https://qyapi.weixin.qq.com/cgi-bin/message/send?access_token=" + access_token;
postHttp(msgUrl, message);
```


* 为保证Tasker稳定运行,请把Tasker加入电池优化白名单.
* 为保证配置正常运行,请赋予Tasker相应的权限.
* 运行不正常,请提供提示信息和运行日志到群内反馈.  
  点击我加入群【Tasker配置分享群】


群二维码

[点我导入配置](https://taskernet.com/shares/?user=AS35m8kcE3fopVGguKw+JP1fYIWaL6G53enhFTrMP6xMnJawIbufv/cr1krqlca25FgFK7KKdWs=&id=Profile:发送未接来电信息到微信)