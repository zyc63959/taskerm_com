---
title: 解析数据
author: 记忆水晶
type: post
date: 2021-06-28T11:00:10+00:00
excerpt: Tasker解析、提取数据的方法说明
url: /2021/06/28/structured-variables.html
keys:
  - 数据,解析,提取数据,提取值,获取值,将提取出来,Tasker,教程
categories:
  - 教程

---
> 在Tasker诞生以来的10多年中，数据解析都是Tasker中最重要的功能，但也是最令人头疼的事。之前的数据解析都是用的 变量搜索替换、变量分割 或者 模式匹配，这些方法使用难度较大，容易出错，还非常麻烦。

从版本5.12开始, Tasker 可以直接解析一些数据类型的字符串(如 JSON ， HTML，XML ， CSV)。

为了能够解析这些数据，在创建变量的操作中选中 数据结构化(Structured Output） 选项(例如:定义变量、 HTTP 请求等)。为了便于使用，Tasker 默认启用该选项。

对于不能解析的变量，启用这个选项也不太可能会产生任何问题，因为如果 Tasker 发现数据类型不符合任何已知的结构化数据，那它也不会去尝试解析数据。这个选项只是一个预防措施，以确保升级不会破坏现有的设置，来兼容旧的配置。

下面是如何解析支持的数据类型的例子。

## JSON

对于下面的 JSON 数据:

```
 {  
     "names":[  
        {  
           "name":"João",  
           "lastname":"Dias"  
        },  
        {  
           "name":"John",  
           "lastname":"Days",  
           "age": 99  
        }  
     ]  
  }
```

可以使用如下所示的圆点符号(也就是.)或方括号符号(也就是[])，(假设上面的文本是一个名为 %json 的变量值)。

  * **%json.name** 或 **%json[name]** 或 **%json.names.name** 将返回第一个叫 **João** 的名字
  * **%json.name() 或** **% json\[name\]()** 或 **%json.names.name()** 将返回一个逗号分隔的名称列表:**João,John**

![](https://oss.taskerm.com/2021/06/json.png!large)

注意:

  1. 仅仅使用键 **name** (在json结构中，冒号前面的字符串称为键，冒号后面的字符串称为值)，将获得该键的第一个值。如果想获得特定完整路径的值，请使用 **names.name** 。
  2. 获取数组将得到所有匹配的值. Tasker并没有使用完整的JSON对象结构，而是简化了数据结构的解析过程，减少了错误；在上面的例子中，%json.age() 的值是 99。
  3. 如果使用点符号(.)，则不能使用无效的 Tasker 变量名字符(字母数字下划等字符)。所以对于不是有效的Tasker变量名只能使用方括号，例如：%json[last name],因为last name中间有而不能使用 %json.last name 的形式
  4. 可以使用 Tasker 的数组功能。例如：可以使用 %json.name(<) 得到 name 中的最后一个值 john.
  5. 在 列表对话框(**List Dialog**)操作中，可以在输入(**input**)区域，可以使用 %json.name，但是因为含有逗号(,)会对原数据造成破坏，而不能或者不建议使用 %json.name() 。

## HTML/XML

对于下面的 HTML 数据:
```html
 <!DOCTYPE html>  
 <html>  
 <head>  
     <title>Test HTML For Tasker</title>  
 </head>  
 <body>  
     <h1>Hello!</h1>  
     <div>How are you?</div>  
     <div>I'm fine!</div>  
     <img src="image.jpg" />  
 </body>  
 </html>
```

可以使用如下所示的圆点符号(也就是.)或方括号符号(也就是[])，(假如上面的文本字符串是一个名为 %html 的变量值)。

  * **%html.div** 或 **%html[div]** 返回第一个 div 的内容: **How are you?**
  * **%html.div()** 或 **%html\[div\]()** 将返回一个逗号分隔的 div 内容列表: **How are you?,I&#8217;m fine!**
  * **%html[img=:=src]** 将返回第一个 img 的 src 属性 。可以使用字符串 **=:=** 检索元素的属性

![](https://oss.taskerm.com/2021/06/html.png!large)

注意:

  1. 如果想使用一个属性**[attr=value]**来匹配 CSS 查询，那么就用花括号{}代替方括号[]。例如**{attr=value}**，查询 **div** 元素属性 **sr=1**，应该用一些 **%html[div{sr=1}]**
  2. 如果想使用一个使用括号的 CSS 查询，比如 **div:nth-child(2)** 使用半角英文符号**«»**(注意：不是书名号《》) 后为：**div:nth-child«2»**
  3. HTML/XML 数据解析不支持在同一表达式中嵌套解析，也就是不能使用 **%html.query1.query2** 。但是可以使用像 query1 > query2一样的 CSS 查询的方式来获取内部字段

## CSV

对于下面的 CSV 数据:
```
 name,age,town  
 Jack,41,London  
 Lindsey,12,New York  
 Eddie,54,Lisbon
```

可以使用如下所示的圆点符号(也就是.)或方括号符号(也就是[])，(假如上面的文本字符串是一个名为 %csv 的变量值)。

  * **%csv.name**或 **%csv[name]** 将返回第一个名字 **Jack**
  * **%csv.name()** 或 **%csv\[name\]()** 将返回一个逗号分隔的名称列表: **Jack,Lindsey,Eddit**

![](https://oss.taskerm.com/2021/06/csv.png!large)

注意:

  1. 如果使用点符号，则不能使用无效的 Tasker 变量名字符。例如: 如果需要用键 **some thing** 解析 CSV 值,必须使用方括号符号 **%csv[some thing]**
  2. 可以使用 Tasker 的数组功能。例如, 可以用 **%csv.name(<)** 得到最后一个名字 **Eddie**
  3. 在 列表对话框(**List Dialog**)操作中，可以在 输入(**input**)区域，可以使用 %csv.name，但是因为含有逗号(，)会对原数据造成破坏，而不能或者不建议使用 %csv.name() 。

最后附上视频演示

