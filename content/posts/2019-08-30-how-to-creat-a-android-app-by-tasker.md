---
title: 在Android手机上使用Tasker制作天气应用
author: 记忆水晶
type: post
date: 2019-08-30T08:24:00+00:00
url: /2019/08/30/how-to-creat-a-android-app-by-tasker.html
featured_image: /wp-content/uploads/2019/08/新建场景-480x300.jpg
views:
  - 121
wpcom_likes:
  - 4
categories:
  - 教程
tags:
  - 场景
  - 天气
  - 应用

---
> 是的,没错! Tasker可以用来制作APP；天气,日历,计算器,记事本等是现代手机的标配,这些APP都是可以通过Tasker来制作的,本篇文章就是以天气应用为例来描述如何制作一款简单的Android APP.

制作之前先想好要实现的功能,设计美观的界面,并找到一个能满足需求的天气源(即提供天气信息的接口，本篇的天气源用的是 彩云天气 )

#### 用Tasker制作一款典型的Android APP一般分为三个步骤: 1.场景制作(界面设计) 2.写配置 3.生成应用

### 一. 场景制作

![][1] 

场景:由场景元素组成的用来显示可交互界面的集合  
在Tasker主界面上点击_场景选项卡_切换到场景查看和制作界面,点击右下的_“+”按钮_新建一个场景,设定_场景名称_后自动进入场景_设计界面_.  

首先,设定场景的基本属性.点击右上的三点式汉堡菜单选择点击属性:

  1. 场景类型有活动，对话框和图层三种

![][2] 

  * 活动,我们常见到的app界面就是活动界面.
  * 对话框,相对于活动 只有对话框上面的控件可以点击,背景暗淡
  * 图层,相当于悬浮窗

  1. 场景大小(水平尺寸和垂直尺寸)和方向(横向布局和竖向布局)
  2. 场景背景色:可以填写颜色值或者变量,也可以点击放大镜按钮选择颜色
  3. 如无需求,其他一般默认即可  

    其次,设定场景网格大小.网格有利于快速对其场景元素,大网格更方便更快速对齐元素,小网格的位置更精确.  
    最后,添加元素,在设计元素的过程中,元素可以被复制,粘贴,删除,隐藏,固定位置,也可以设定深度,或者设为背景元素来铺满整个场景.  
    最常用的元素:矩形,文本,可编辑文本,按钮,图片,菜单

  * 矩形:常来布局场景元素,设定场景整体背景和局部背景,也可以用来设定一组元素的共同行为(action)
  * 文本:不可编辑的标签
  * 可编辑文本:文本框
  * 按钮:常用的用来响应单击,长按等操作的行为
  * 图片:用来显示图片的元素
  * 菜单:常用来当做显示数组的文本标签

按照设计的尺寸大小和位置,添加各个元素到场景中

![场景界面][3] 


右下角的放大镜按钮可以用来切换场景的状态(1.设置场景相对于手机屏幕的布局,2.设置场景内的元素)

![触摸模式-选择模式][4] 


下中的”+”用于添加场景元素

![新建模式-预览模式][5] 


下左的手掌图标用于选择触摸的模式(正常,编辑,移动,调整大小)，一般选择正常。

下左的”AZ”列出了场景中所有的元素，长按列表中的选项，可以对元素进行删除,复制,焦点,设置深度,设置背景,钉住和隐藏。

![元素编辑][6] 

### 二. 写配置（即逻辑配置）

关于数据解析，如果你会任何编程语言的话，理解起来比较容易，如果不会也没有关系，同样可以实现：

![任务编辑][7] 


既可以使用JS中关于JSON对象的方法来实现，也可以使用Tasker自带的搜索替换功能来实现。

  1. 使用JS实现如下


```javascript
var cytoken=”2zHu=DbPVTvusLnq”;  
var amapkey=”8c74fc85bfcd90e7df82fafd5097b40d”; //定义get方法  
function gethttp(url) {  
var xhr = new XMLHttpRequest();  
xhr.addEventListener(“readystatechange”,  
function() {  
if (this.readyState === 4) {  
//flash(this.responseText); //显示返回消息,可删除本行  
}  
});  
xhr.open(“GET”, url, false);  
xhr.send();  
return xhr.responseText;  
} //通过网络获取手机坐标GPS  
var lastFix = getLocation(‘net’, true, 10);  
var loc = global(‘%LOCN’).split(“,”); //手机坐标GPS转换为高德坐标  
var loc0 = Number(loc\[1\]).toFixed(6);  
var loc1 = Number(loc\[0\]).toFixed(6);  
var convertUrl = “http://restapi.amap.com/v3/assistant/coordinate/convert?locations=” + loc0 + “,” + loc1 + “&coordsys=gps&output=json&key=”+amapkey;  
var amapLoc = JSON.parse(gethttp(convertUrl)).locations.split(“,”); //根据坐标获取当前行政区域信息  
var loc0 = Number(amapLoc\[0\]).toFixed(6);  
var loc1 = Number(amapLoc\[1\]).toFixed(6);  
var regeoUrl = “http://restapi.amap.com/v3/geocode/regeo?output=json&location=” + loc0 + “,” + loc1 + “&key=”+amapkey+”&radius=100&extensions=all”  
var result = JSON.parse(gethttp(regeoUrl));  
var addressComponent = result.regeocode.addressComponent;  
var contry = addressComponent.contry;  
var province = addressComponent.province;  
var city = addressComponent.city;  
var district = addressComponent.district;  
var townshipy = addressComponent.township;  
var name = result.regeocode.pois\[0\].name;  
var address = result.regeocode.pois\[0\].address; //flash(townshipy + name);//提示街道和小区名 //获取小时天气数据  
var loc0 = Number(loc\[1\]).toFixed(4);  
var loc1 = Number(loc\[0\]).toFixed(4); var weatherUrl = “https://api.caiyunapp.com/v2/”+cytoken+”/” + loc0 + “,” + loc1 + “/hourly.json” //解析天气数据  
var result = JSON.parse(gethttp(weatherUrl));  
var hourly\_description = result.result.hourly.description;  
var forecast\_keypoint = result.result.forecast\_keypoint;  
var wind = result.result.hourly.wind\[0\].speed + ” km/h”;  
var humidity = result.result.hourly.humidity\[0\].value + ” %”;  
var pmmm = result.result.hourly.pm25\[0\].value;  
var skycon = result.result.hourly.skycon;  
var skycon0 = skycon\[0\].value;  
var temperature = result.result.hourly.temperature;  
var temperature0 = temperature\[0\].value + ” ℃”;  
var pm25 = result.result.hourly.pm25;  
var pm250 = pm25\[0\].value; var weather={“CLEAR\_DAY”:”晴（白天）”,”CLEAR\_NIGHT”:”晴（夜间）”, “PARTLY\_CLOUDY\_DAY”:”多云（白天）”, “PARTLY\_CLOUDY\_NIGHT”:”多云（夜间）”, “CLOUDY”:”阴”, “RAIN”:”雨”, “SNOW”:”雪”, “WIND”:”风”, “FOG”:”雾”, “HAZE”:”霾”, “SLEET”:”冻雨”};  
var skyconurl = {  
“CLEAR\_DAY”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_image\_wb\_sunny”,  
“CLEAR\_NIGHT”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_image\_brightness\_3”,  
“PARTLY\_CLOUDY\_DAY”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_file\_cloud\_queue”,  
“PARTLY\_CLOUDY\_NIGHT”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_file\_cloud\_queue”,  
“CLOUDY”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_image\_wb\_cloudy”,  
“RAIN”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_places\_beach\_access”,  
“SNOW”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_places\_ac\_unit”,  
“WIND”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_device\_grapheq”,  
“FOG”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_action\_line\_weight”,  
//以下暂未提供  
“HAZE”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_places\_all\_inclusive”,  
“SLEET”: “android.resource://net.dinglisch.android.taskerm/drawable/mw\_places\_beach\_access”  
} var hourtime = \[48\];  
var sky = \[48\];  
for (o in skycon) {  
sky\[o\]=weather\[skycon\[o\].value\];  
hourtime\[o\] = skycon\[o\].datetime.substring(11)  
}; var pmm = \[48\];  
for (o in pm25) {  
pmm\[o\] = pm25\[o\].value + ” pm2.5″;  
}; var temp = \[48\];  
for (o in temperature) {  
temp\[o\] = temperature\[o\].value + ” ℃”;  
}; var mweather=\[48\]; const fill=(c,l)=>t=> \`${t}${c.repeat(l)}\`.substring(0,l);  
for (var i=0;i<48;i++) {  
mweather\[i\] =\[hourtime\[i\],sky\[i\],pmm\[i\],temp\[i\]\].map(fill(‘\*’,8)).join(”);  
}  
var weatherconurl=skyconurl\[skycon\[0\].value\]  
var now = new Date((result.server\_time) \* 1000);  
var server\_time = (now.getHours()<10 ? “0” + now.getHours() : now.getHours()) + “:” + (now.getMinutes()<10 ? “0” + now.getMinutes() : now.getMinutes());  
console.log(server\_time);  
```

  1. 使用Tasker自带的变量拆分，变量搜索替换，设置数组等一系列操作也可以完成，具体可参考其他人分享的天气示例。

> 运行一次刚刚制作的配置，看看是否运行正常。



### 三. 生成应用

首先，安装Tasker对应版本的app factory这款应用（仅仅安装好就可以了）。

> app factory的版本号需要和Tasker的版本号严格对应，否则生成应用时会提示错误

>

然后，打开Tasker菜单>更多>开发人员选项>创建证书，来为应用生成一个签名，这一步很简单，按照提示操作就行了。注意设置一个简单好记的密码。

其次，切换到Tasker任务选型卡，长按刚刚创建的任务配置，点击右上菜单，选择导出>作为应用  
设置以下选项

  1. 包名，类似于：com.android.appname 这种格式的；
  2. 版本名，例如：1.0
  3. 启动任务，可以点击右边的搜索按钮找到

以上三个选项设置好以后，点击手机返回按钮或者左上的返回按钮，这样Tasker就开始自动生成应用了。  
安装刚刚生成的天气应用，打开就可以看到我们设计的天气应用界面了。

[1]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/%E6%96%B0%E5%BB%BA%E5%9C%BA%E6%99%AF.jpg
[2]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/尺寸_场景属性.jpg?x-oss-process=image/resize,m_fill,h_909,w_1024
[3]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/场景属性_场景界面.jpg?x-oss-process=image/resize,m_fill,h_909,w_1024
[4]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/触摸模式_选择模式.jpg?x-oss-process=image/resize,m_fill,h_909,w_1024
[5]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/新建模式-预览模式.jpg?x-oss-process=image/resize,m_fill,h_909,w_1024
[6]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/元素编辑_菜单编辑.jpg?x-oss-process=image/resize,m_fill,h_909,w_1024
[7]: https://ishare-cf.oss-cn-hongkong.aliyuncs.com/2019/09/任务编辑-操作.jpg?x-oss-process=image/resize,m_fill,h_909,w_1024