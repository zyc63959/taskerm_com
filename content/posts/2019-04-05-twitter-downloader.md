---
title: 用Tasker解析Twitter视频地址
author: 记忆水晶
type: post
date: 2019-04-05T21:04:00+00:00
url: /2019/04/05/twitter-downloader.html
views:
  - 495
categories:
  - 教程
tags:
  - twitter

---
## 前言

使用Tasker制作Twitter下载器跟制作其他网站的下载器有所不同,这是因为Twitter网页本身并没有可以解析到的视频下载地址.

## 原理和步骤

借用Twitter官方提供的[api](https://api.twitter.com/1.1/statuses/show.json)来下载视频 点击这里注册一个Twitter开发者账号:[https://developer.twitter.com](https://developer.twitter.com) 
有了账号后会提供开发用到的token来用于认证,把你的token替换掉文末的代码中就可以用了.

## 使用方法:

  1. 复制带视频的推文链接
  2. 复制视频播放时的视频地址

## 代码

```javascript
var token="AAAAAAAAAAAAAAAAAAAAABXesyegAAAAAA2mJuTUyoBiQiFqw9KIVwOZPoELi/N=djisfUIdUdIiIsU1ILUxIUI2UdIUIUuilljle0yH1LL232X";

var clip=global('CLIP')
var idpatt=/\d{19}/;
var id=idpatt.exec(clip);
var url="https://api.twitter.com/1.1/statuses/show.json?id=" + id[0] + "&tweet_mode=extended";

function gethttp(url,token) {
    var xhr = new XMLHttpRequest();
    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === 4) {
           //flash("成功获取数据");//显示返回消息,可删除本行
        }
    });
    xhr.open("GET", url, false);
    xhr.setRequestHeader("Authorization", "Bearer " + token);
    xhr.send();
    return xhr.responseText;
}

var json=JSON.parse(gethttp(url));

var variants=json.extended_entities.media[0].video_info.variants;

var max=0; 
var videourl;

for (var i=0;i&lt;variants.length;i++){

    var bitrate=variants[i].bitrate
    if(bitrate){
        if(bitrate&gt;max){
            max=bitrate;
            videourl=variants[i].url
        }


    }


}

flash(videourl);
```

## 说明

这样就可以解析出Twitter视频的下载地址(解析出来的时最大清晰度的地址)  
有了地址就可以下载了,如果你想了解如何下载可以参考[这篇文章][1]

[1]: https://taskerm.com/2019/03/26/instagram-downloader/