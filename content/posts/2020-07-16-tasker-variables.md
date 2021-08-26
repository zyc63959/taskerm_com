---
title: Tasker教程之变量
author: 记忆水晶
type: post
date: 2020-07-16T09:04:21+00:00
url: /2020/07/16/tasker-variables.html
views:
  - 327
categories:
  - 教程

---
## 概述

变量是一个随时间变化的命名值，例如电池电量，一天中的时间。

当Tasker在文本中遇到变量名称时，它将在执行操作之前用相关变量的当前值替换名称。

变量的主要目的是：

* _动态绑定_：对数据进行操作创建任务（例如响应SMS）时未知；直到收到SMS，发送者才被知道。
* 允许在任务内部和任务之间 进行[流控制](https://tasker.joaoapps.com/userguide/en/flowcontrol.html)[https://tasker.joaoapps.com/userguide/en/flowcontrol.html](https://tasker.joaoapps.com/userguide/en/flowcontrol.html)
* 记录数据以备将来使用，例如在任务之间传递数据

## 全局变量与局部变量

具有**全小写**名称的变量（例如％fruit_bar）是_局部变量_，这意味着它们的值特定于使用它们的任务或场景。名称中具有一个或多个大写字母的变量（例如，％Car，％WIFI）是_全局_变量，这意味着从任何地方访问它们都将返回相同值。

## 内置变量

Tasker自动更新内置变量的值。

### 本地内置变量

* **操作错误**  
    _％err_  
    如果运行最后一个操作时发生错误，则设置为整数。实际数字可以表示发生的错误，但对于大多数Tasker动作（值得注意的例外：`Run Shell`和插件）通常为1 。每个动作都会设置或清除它，因此，如果要在紧接着的下一个动作之后需要它，则必须将其保存（例如：使用[Variable Set](https://tasker.joaoapps.com/userguide/en/help/ah_set_variable.html)）。 [https://tasker.joaoapps.com/userguide/en/help/ah\_set\_variable.html](https://tasker.joaoapps.com/userguide/en/help/ah_set_variable.html)
* **操作错误描述**  
    *％errmsg ***最后导致设置％err**的错误的描述。当前从未由Tasker设置，但可能由某些插件操作设置。
* **任务优先级**  
    _％priority_  
    正在运行的任务的优先级。当多个任务一起运行时，优先级确定哪个任务将执行下一个动作。另请参阅：[任务计划](https://tasker.joaoapps.com/userguide/en/tasks.html#scheduling)  
    [https://tasker.joaoapps.com/userguide/en/tasks.html#scheduling](https://tasker.joaoapps.com/userguide/en/tasks.html#scheduling)
* **任务队列时间**  
    _％qtime_  
    运行中的任务已经运行了多长时间（秒）。 请注意，优先级较高的任务可能会中断任务，因此此数字不一定是任务的总运行时间。
* **任务调用者**  
    _％caller_  
    一个变量数组，用于跟踪当前正在运行的任务的来源。_％caller1_给出当前任务的来源，_％caller2_给出*％caller1_的来源，依此类推。示例：如果任务A使用动作`Perform Task`启动任务B，则在任务编辑屏幕中按“播放”按钮运行任务A时，任务B中的_％caller1_将显示**task = A**，_％caller2_将显示**ui**。数组中每个条目的格式为_callertype*（**= **_callername_（**：**_subcallername_））呼叫者类型如下：
* **配置文件**  
    一种配置（状态更改时）。根据配置文件是已激活还是已停用，_呼叫者_名称是**进入**还是**退出**。_subcallername_是配置文件的名称（如果有），否则为**匿名**
* **场景**  
    场景事件，其中_callername_为场景名称。对于元素事件，_subcallername_是元素名称。对于按下操作栏按钮，如果指定了\*\*subcallername\* ，_则该_subcallername* 为标签。对于场景全局事件（例如Key），_subcallername_ _名称_为事件类型
* **ui**  
    Tasker UI中任务编辑屏幕中的“播放”按钮
* **启动**  
    点击启动子应用程序图标
* **nbutton**  
    一个通知操作按钮，可以从Tasker的永久通知中使用，也可以通过“通知”操作之一创建。 _呼叫者名称_指定按钮的标签（如果存在）。
* **外部**  
    外部应用（注：第三方应用）
* **qstile**  
    快速设置磁贴。_callername_指定磁贴的标签。（注：下拉状态栏中的快捷设置）。
* **appshort**  
    应用程序快捷方式（可通过长按Tasker图标来访问）。_callername_指定图块的标签。
* **任务**  
    一个任务，从执行任务的行动。_subcallername_是任务名称（如果有），否则为**匿名**

### 全局内置变量

* **飞行模式状态**`(dynamic)`  
    _％AIR_  
    飞行模式是**打开**还是**关闭**
* **飞行无线通讯**  
    _％AIRR_  
    以逗号分隔的无线通讯列表，进入飞行模式后将被**禁用**。 常见的无线通讯名称是：_蓝牙，蜂窝网络，nfc，wifi，wimax_。
* **电池电量**  
    _％BATT_  
    当前设备的电池电量从0到100。
* **蓝牙状态** `(dynamic)`  
    _％BLUE_  
    蓝牙是**处于打开**状态还是处于其他状态（**关闭**）。
* **日历列表**  
    _％CALS_  
    设备上可用的以换行符分隔的日历列表。 每个条目的格式为_calendarprovider：calendarname_。 用法示例： Variable Set, %newline, \\n Variable Split, %CALS, %newline Flash, %CALS(#) calendars, first one is %CALS(1)
* **日历事件标题/说明/位置***％CALTITLE /％CALDESCR /％CALLOC *  
    **当前**日历事件的标题，描述和位置（如果有）。如果当前有多个日历事件，则变量指的是**最短的**事件。 提示：使用Misc / Test操作（为数据指定％TIMES ）查找有关当前事件的其他详细信息。
* **呼叫名称/号码/日期/时间（拨打）**`(dynamic, monitored)`  
    _％CNAME /％CNUM /％CDATE /％CTIME_  
    当前（如果正在通话中）或最近一次呼叫的呼叫者姓名，号码，日期和时间。如果未知，则 主叫号码为**0**。 来电者姓名是**？**（如果是未知的）（可能是因为呼叫者号码被阻止），如果找不到联系人，则将其设置为呼叫者号码。在2.0之前的Android版本上不可用。
* **呼叫名称/号码/日期/时间/持续时间（接听）**`(dynamic, monitored)`  
    _％CONAME /％CONUM /％CODATE /％COTIME /％CODUR_  
    上次（**不是**当前）呼出电话的被叫名称，号码，日期和时间。 如果无法查找联系人，则“被叫姓名”设置为被叫号码。在2.0之前的Android版本上不可用。
* **小区ID **`(monitored,dynamic)`  
    _％CELLID_  
    当前的小区信号塔ID（如果知道）。 如果使用的是Cell Near状态，则即使％CELLID报告塔ID未知或无效，有时Cell Near状态也会保持活动状态。这是因为Cell Near仅响应有效ID，以防止状态（例如由于服务中断）变为非活动状态。 为了向后兼容，将使用GSM前缀报告UMTS小区。 从Android 4.2（塔斯克版4.3+版本）开始，可以同时从2种不同的网络类型中找到单元。在这种情况下，该值优先报告列表中最左边的网络类型：GSM，CDMA，UMTS，LTE。
* **信元信号强度**`(monitored,dynamic)`  
    _％CELLSIG_  
    在粗糙的线性范围内，当前电话信号电平介于0到8之间。在某些手机上，级别将以2（0、2、4、6、8）为步长上升。如果该值未知或没有服务，则该值为-1。 从Android 4.2（塔斯克版4.3+版本）开始，可以同时从2种不同的网络类型中找到单元。在这种情况下，该值优先报告列表中最左边的网络类型：GSM，CDMA，UMTS，LTE。 某些Android版本存在一个错误，即在设备关闭和打开之前，报告的信号强度不会更新。
* **小区服务状态**`(monitored,dynamic)`  
    _％CELLSRV_  
    当前电话服务状态：_未知的，服务状态，无服务，紧急情况下，无电_。（_unknown, service, noservice, emergency, nopower_）
* **剪贴板内容**`(monitored,dynamic)`_％CLIP_  
    系统剪贴板的当前内容。请注意，牢牢锁定设备屏幕时无法访问剪贴板。
* **CPU频率**  
    _％CPUFREQ_  
    当前以CPU 0运行的频率。另请参阅：[CPU控制](https://tasker.joaoapps.com/userguide/en/cpu.html)。[https://tasker.joaoapps.com/userguide/en/cpu.html](https://tasker.joaoapps.com/userguide/en/cpu.html)
* **CPU调速器**  
    _％CPUGOV_  
    当前的调速器控制CPU 0的频率。另请参见：[CPU控制](https://tasker.joaoapps.com/userguide/en/cpu.html)。[https://tasker.joaoapps.com/userguide/en/cpu.html](https://tasker.joaoapps.com/userguide/en/cpu.html)
* **日期**  
    _％DATE_  
    当前人类可读的日期。
* **当月的当前天数**  
    _％DAYM_  
    每月的当天日期，从1开始。
* **星期数**  
    _％DAYW_  
    当前的**星期数**，从星期日开始。
* **设备ID /制造商/型号/产品**  
    _％DEVID /％DEVMAN /％DEVMOD /％DEVPROD_  
    设备的ID，制造商，型号和产品名称。注意：ID **不是设备**的唯一标识符，而是设备的硬件。另请参阅：％DEVTID。
* **设备电话ID**  
    _％DEVTID_  
    返回设备的唯一基于电话的ID（例如，对于GSM，IMEI，对于CDMA，MEID或ESN）。并非在所有设备上都可用。
* **显示亮度**  
    _％BRIGHT_  
    当前屏幕亮度，0-255。在某些设备上，如果启用了Android设置“自动亮度”，则该值将始终为255。
* **显示超时**  
    _％DTOUT_  
    当前系统屏幕超时（秒）。
* **电子邮件发件人/抄送/主题/日期/时间**`(dynamic)`  
    _％EFROM /％ECC /％ESUBJ /％EDATE /％ETIME_  
    K9电子邮件代理收到的最后一封电子邮件的发件人，抄送，主题，接收日期和接收时间。
* 可用**内存**  
    _％MEMF_  
    系统剩余可用内存，以MB为单位。
* **GPS状态**  
    （受监视的动态姜饼+） _％GPS_ 系统GPS接收器是**打开**还是**关闭**。
* **心率**`(monitored,dynamic)`  
    _％HEART_  
    当前检测到的心率，每分钟心跳数。 另请参阅：状态_心率_。 对于无接触（-1），精度不可靠（-2）或其他问题（-3），该值为负
* **HTTP响应代码/数据/内容长度**`(dynamic)`_％HTTPR /％HTTPD /％HTTPL_  
    来自上一个HTTP POST / GET操作的值。 如果服务器未返回内容长度，则将在可能的情况下根据返回的数据计算％HTTPL。
* **湿度**`(monitored,dynamic)`  
    _％HUMIDITY_  
    相对环境空气湿度，以百分比为单位。 另请参阅：状态_湿度_。
* **输入法**  
    _％IMETHOD_  
    当前有效的输入法。由4个部分组成，以逗号分隔：方法名称，子类型名称，模式，语言环境。 要访问特定零件，请使用“ *可变拆分”*操作。
* **中断模式**`(dynamic)`  
    _％INTERRUPT_  
    仅在Android 5.0+上可用，**要求启用Tasker的通知访问服务**，请参阅Android的“声音和通知”设置。 Android 5.0+：设备上的中断模式的当前状态：**none**，**优先级**或**全部**请参见：动作_中断模式_ Android 6.0+：设备上的“请勿打扰”模式的当前状态：**none**，**priority**，**全部**或**警报**请参见：动作_请勿打扰_
* **键盘锁状态**  
    _％KEYG_  
    键盘锁是**打开**还是**关闭**
* **上一个应用程序**  
    _％LAPP_  
    当前应用程序之前位于前台的应用程序的名称，例如Maps。
* **最后一张照片**  
    _％FOTO_  
    Tasker或标准系统相机应用程序拍摄的最后一张照片的文件系统路径。
* **照明度**`(monitored,dynamic)`  
    _％LIGHT_  
    最后记录的照明度（勒克斯）。请注意，直到光线水平发生变化，Android才会返回值，因此要测试传感器是否正常工作，应首先将其放在明亮的光线下。 关闭设备显示屏时，可能不会更改，请参阅。  
    `Menu / Prefs / More / Display Off Monitoring / Light Sensor`
* **位置**`(dynamic)`  
    _％LOC_  
    最近一次GPS定位的纬度和经度。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **定位精度**`(dynamic)`  
    _％LOCACC_  
    最近一次GPS定位的精度（以米为单位）。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **位置高度**`(dynamic)`  
    _％LOCALT_  
    最近一次GPS定位的高度（以米为单位）；如果不可用，则为0。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **定位速度**`(dynamic)`  
    _％LOCSPD_  
    上一次GPS定位的速度，以米/秒为单位；如果不可用，则为0。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **位置定位时间秒数**`(dynamic)`  
    _％LOCTMS_  
    最近一次GPS定位的时间（以秒为单位）。要获取修复时间，请远离％TIMES。 在计算出GPS时间相对于固定时间的偏移之前（应该在第一次GPS定位之后），才设置此值，因为该值在该点之前是无意义的。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **位置（净值）**`(dynamic)`  
    _％LOCN_  
    最近一次网络位置修复的纬度和经度。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **位置精度（净值）**`(dynamic)`  
    _％LOCNACC_  
    最近一次网络位置**定位的精度（**以米为单位）。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **位置定位时间（净值）**`(dynamic)`  
    _％LOCNTMS上_  
    一次**网络位置定位的时间（**以秒为单位）。要获取修复时间，请远离％TIMES。 [请参阅注释](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)。  
    [https://tasker.joaoapps.com/userguide/en/variables.html#locnote](https://tasker.joaoapps.com/userguide/en/variables.html#locnote)
* **磁场强度**`(monitored,dynamic)`  
    _％MFIELD_  
    作用在设备传感器所有三个轴上的磁场的微_特拉斯拉_总强度。 每秒更新一次。另请参见：state 。  
    `Magnetic Field`
* **音乐曲目**`(monitored,dynamic)`  
    _％MTRACK_  
    当前播放的音乐曲目，支持：
* Tasker动作_音乐播放_和_音乐播放目录_
* 内置的Android音乐播放器，可能不是在所有设备上都可以
* 功率放大器
* BeyondPod（塔斯克v1.2.1 +）
* 幻影音乐控制专业版
* 媒体工具优先：如果同时播放Tasker和其他受支持的应用程序之一，则将显示非Tasker曲目。如果同时运行多个其他受支持的应用程序，则行为未指定。 笔记：
* 如果没有受支持的播放器，则可以尝试Phantom Music Control Pro或Media Utilities，它们支持很多播放器，应将信息传递给Tasker
* 暂停曲目会清除变量，取消暂停会再次设置它
* 您的音乐播放器可能需要启用一个选项才能广播曲目信息，或者广播只能以“专业”版本提供
* **静音**  
    _％MUTED_  
    麦克风当前是否处于静音状态（**打开**）（**关闭**）。
* **夜间模式**  
    _％NIGHT_  
    当前的Android夜间模式。 一**对**，**关闭**或**自动**。 如果为**auto**，Android将自行决定是否应处于夜间模式。
* **通知标题**`(monitored, dynamic)`  
    _％NTITLE_  
    状态栏中显示的最后一条通知的标题。在使用KitKat之前，需要运行Tasker的辅助功能服务器（请参阅Android辅助功能设置）。在KitKat中，需要运行Tasker的Notification Listener服务。 在由于或事件而运行的任务中，请使用变量％evtprm2而不是％NTITLE。这更加可靠，您可以访问通知的其他部分（％evtprm3等） ，但不显示Tasker生成的通知。  
    `NotificationNotification Removed`
* **电话号码**  
    _％PNUM_  
    设备_正在_使用中的当前电话号码。 在某些手机上，它不起作用（Android限制），似乎与SIM卡的类型有关。
* **压力**`(monitored,dynamic)`  
    _％PRESSURE_  
    设备上的当前气压（以毫巴为单位）。 关闭设备显示屏时，可能不会更改，请参阅。  
    `Menu / Prefs / Monitor / Display Off Monitoring / Pressure Sensor`
* **活动配置文件**`(dynamic)`  
    _％PACTIVE_  
    以激活顺序列出的当前活动的命名配置文件的逗号分隔列表。重复的名称只会在列表中出现一次。该列表始​​终以逗号开头和结尾，以使匹配更容易（如果不为空）。
* **已启用配置文件**`(dynamic)`  
    _％PENABLED_  
    按创建顺序，以逗号分隔的当前启用的命名配置文件列表。重复的名称只会在列表中出现一次。该列表始​​终以逗号开头和结尾，以使匹配更容易（如果不为空）。
* **漫游**  
    _％ROAM_  
    **上**如果装置在当前电话网络上漫游，否则**关闭**。
* **Root Available**  
    _％ROOT_  
    **是**如果此设备上具有root功能，则为**yes**，否则为**no**。
* **屏幕**`(dynamic)`  
    _％SCREEN_  
    屏幕是打开（值**on**）还是关闭（值**off**）。
* **SDK版本**  
    _％SDK设备_  
    的数字Android [SDK版本](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html) 。[http://developer.android.com/reference/android/os/Build.VERSION_CODES.html](http://developer.android.com/reference/android/os/Build.VERSION_CODES.html)
* **静音模式**`(dynamic)`  
    _％SILENT **静音模式**  
    的当前状态：**关闭**，**振动**或打开_。 在Android 5.0及更高版本中，此变量仅用于反映设备是否处于振动模式（**vibrate**）（不是）（任何其他值），但是包含**on**值是为了向后兼容，并且在设备不处于振动模式时进行设置，并且中断模式为**无** 或**优先**。 另请参见：变量*％INTERRUPT*，操作_静默模式_和_中断模式_。
* **SIM序列号**  
    _％SIMNUM_  
    SIM卡的序列号（如果存在且可访问）。 如果SIM卡尚未解锁，将无法使用。
* **SIM卡状态**  
    _％SIMSTATE_  
    SIM卡的当前状态：**unknown, absent, pinrequired, pukrequired, netlocked or ready**。
* **免提**  
    _％SPhone_  
    扬声器是**开启**或**关闭**
* **语音**`(dynamic)`  
    _％SPEECH_  
    （如果适用）由于“ *播报”*或“ *播报到文件”*操作而导致的当前讲话。
* **正在运行的任务**`(dynamic)`  
    _％TRUN_  
    当前正在运行的任何被命名的任务的逗号分隔列表。该列表始​​终以逗号开头和结尾，以使匹配更容易（如果不为空）。
* **电话网络**`(dynamic, monitored)`  
    _％TNET_  
    设备正在使用的当前电话网络运营商。 在CDMA网络上可能不可靠
* **温度**`(monitored,dynamic)`  
    _％TEMP_  
    当前环境温度，以摄氏度为单位。 关闭设备显示屏时，可能不会更改，请参阅。 另请参阅：状态_温度_。  
    `Menu / Prefs / Monitor / Display Off Monitoring / Temp. Sensor`
* **文本来自/日期/主题/时间**`(monitored)`  
    _％SMSRF /％SMSRN /％SMSRB /％MMSRS /％SMSRD /％SMSRT_  
    接收到的最后一个文本（SMS或MMS）的发件人地址，名称，正文，主题，日期和时间。 这些变量在被引用后将一直为空，直到第一次收到文本为止，因为Tasker不会监视文本，除非需要它。_名称_设置为发件人地址，无法查找任何联系人。在2.0之前的Android版本上不可用。 _车身_（％SMSRB）只设置短信。 仅为MMS设置_主题_（％MMSRS）。
* **时间**  
    _％TIME_  
    当前人类可读的时间，以句点分隔，例如10.59
* **网卡**（动态）   
    _％TETHER_  
    网卡以逗号分隔的列表，即在其另一设备可以连接到这一个，以便使用它的互联网连接连接。 可能的形式是**wifi**，**usb**或**bt**。 仅当通过BT连接实际客户端以使用设备网络连接时，才会出现BT，而在启用该功能后（Android错误/限制）将立即出现其他客户端。
* **Time MilliSeconds**  
    _％TIMEMS_  
    当前时间（以毫秒为单位）。（自1970年1月以来的毫秒数，如果您必须知道的话）。
* **时间秒数**  
    _％TIMES_  
    当前时间，以秒为单位。（如果您必须知道的话，自1970年1月以来的秒数）。
* **UI模式**`(monitored,dynamic)`  
    _％UIMODE_  
    当前的Android UI模式。 其中的**汽车**，**办公桌**，**家电**，**电视**（电视），**手表**，**民主基金**（未定义）或**正常**。
* **正常运行时间秒数**  
    _％UPS_  
    自设备上次启动以来的秒数。
* **音量-警报/呼叫/ DTMF /媒体/通知/铃声/系统**`(dynamic)`  
    _％VOLA /％VOLC /％VOLD /％VOLM /％VOLN /％VOLR /％VOLS_  
    当前音频通道的音量级别。 在某些设备上，音量变化不会动态获取，而在其他设备上，使用电话应用程序时则不会动态变化。
* **WiFi信息**  
    _％WIFII_  
    连接到接入点（AP）时，显示有关该AP的人类可读数据。未连接时，显示附近AP的最新Wifi扫描结果的详细信息。 在Android 8.1+上，可能需要在Android设置中启用基本位置信息服务。
* **无线状态**`(dynamic)`  
    _％WIFI_  
    无论无线网络连接**上**或**关闭**。注意：如果WiFi是启用或禁用的，实际上除了启用以外的任何功能，都将其分类为关闭。
* **Wimax状态**  
    _％WIMAX_  
    Wimax是**打开**还是**关闭**。注意：如果Wimax是启用或禁用的，实际上除了启用以外的任何功能，都将其分类为关闭。
* **窗口标签**`(monitored,dynamic)`  
    _％WIN_  
    当前窗口的标签，可以是全屏活动或对话框。 如果标签未知，则不设置。 对于某些窗口，标签可能是窗口中第一项的标签，例如菜单项或按钮。

### 一般注意事项

上面列表中标记`dynamic`的_变量_会在_变量值_状态和_变量集_事件发生变化时触发更改。

标记`monitored`的变量在窗口小部件或已**启用的**配置文件或任务时，将导致相关监视器启动以跟踪其状态。例如，在Flash操作中使用的％CELLID将导致跟踪单元位置。

限制：匿名快捷方式中无法检测到监视的变量。

### 关于位置变量的注意事项

当位置上下文的相关提供程序（Net或GPS）处于活动状态时，这些变量将报告该提供程序的值，如果其他应用程序正在请求位置，则这些值可能比Tasker所看到的要新。

当相关提供者**未**处于活动状态时，这些变量将报告**Tasker看到**的最后一个值，这可能是`Get Location`操作或监视的结果`Location Context`。

这意味着，如果您在两次使用变量之间关闭了位置提供程序，则报告的修复时间可能**会倒退**。

还可以通过运行`Get Location`操作来手动更新位置变量。

## 用户变量（User Variables）

动作_设置变量_（以及其他几个_变量_）可用于创建新变量。变量名称具有以下限制：

* 他们必须以**％**字符开头
* 他们区分大小写
* 然后必须至少再输入**3**个字母数字字符
* 它们还可以包含下划线字符（_），但不能以下划线字符开头或结尾

通常，最好使用局部变量，因为：

* 您知道他们不会受到其他任务或场景的干扰
* 它们在几种方面更有效

注意：同一任务同时运行的多个副本，每个都有各自的局部变量副本。

### 场景局部变量

每个场景都有自己的局部变量集，这些局部变量与创建场景的任务共享；场景和任务都可以看到对两者所做的变量的更改。

由于场景事件（例如，在元素上点击）而启动的任何任务也共享场景的变量（因此也共享创建场景的原始任务的变量）。

结果，由场景事件（例如，在元素上点击）开始的任务（例如通过“ ***显示场景**”*动作显示新场景）将导致第二场景共享第一场景的变量。

当任务显示由其他任务（或同一任务的不同副本）创建并随后隐藏的场景时，该任务的变量将被**复制**到场景变量（已存在的变量的替代值）中，但该任务**不会共享**场景变量，看不到对其的更改。

### 转义变量名

如果要防止替换变量名，请在其前面放一个\\，例如

> `Variable Set, %new, \%old`

将设置*%new_的值为_%old*，而不是*%old*的值。

为了在变量名前加上****，可以使用转义反斜杠，例如

> `Variable Set, %new, \\%old`

将％new_的值设置为/并且后面是％old_的**值**。

### 变量引用

通过在变量名称的开头添加一个或多个额外的**%**符号，可以间接引用变量。例如：

> `Variable Set, %colour, red Variable Set, %varname, colour Flash %%varname`

…将toast提示**红色**。

使用这种表示法，可以分配名称事先未知的变量：

> `Read File, variablename.txt, To Var, %varname Variable Set, %%varname, red`

这会将名称存储在文件中的变量设置`variablename.txt`为**red**。

您可以根据需要深度嵌套引用（例如`%%%%var`），但是肯定会出现精神压力和错误。

如果链的任何部分的变量名无效，则将返回原始引用。在第一个示例中，如果`%varname` 设置为`!!!`，则将提示`**%%varname**` ，而不是**red**。

### 变量周期

如果未通过任何任务更改**全局**变量 的值，则该值将持续到卸载Tasker为止。

**局部**变量在创建它们的任务结束时丢失，或者在从场景调用的任务中父场景被销毁时丢失。

### 未初始化的变量

没有分配值的用户变量不会进行替换，例如，在表达式“ _我爱％fruit”中_，如果未初始化“％fruit”，则表达式保持原样，否则将“％fruit”替换为该值。

例外：数学表达式中使用的未初始化变量将替换为0。

## 插件中的变量

插件开发人员可以告诉Tasker用其当前Tasker值替换在插件字符串中找到的变量。如果您有不支持此功能的插件，请向开发人员发送此URL

> [http://tasker.dinglisch.net/plugins.html](http://tasker.dinglisch.net/plugins.html)

其中有相关的详细信息。

## 可变数组

Tasker支持伪数组。

当与`For`操作一起使用时，它们特别有用，因为您可以依次对每个元素执行一组操作，例如列出一组文件然后测试每个文件。

### 例子

如果四个变量**％arr1，％arr2，％arr3，％arr4**分别持有**a，b，c**和**d，** 那么我们就有一个包含4个_元素_的数组。这些变量可以像其他变量一样使用，但是也可以通过特殊方式访问它们。这里有些例子：

* **％arr(#)**  
    定义的数组元素的数量（本例中为**4**）
* **％ARR(＃>)**  
    第一个被定义的数组元素的索引值，如果没有被定义时为**0**（本例中为**1**）。
* **％ARR(＃<)**  
    最后一个被定义的数组元素的索引，如果没有被定义时为**0**（本例中为**4**）
* **％ARR(＃？b / c)**  
    数组索引的逗号分隔列表（从最低到最高），带有匹配值；如果不匹配，则返回**0**（在示例中为**2,3**）
* **％ARR(＃？〜Rregex here)**  
    与上面相同，但具有正则表达式匹配
* **％ARR(>)**  
    第一个被定义的数组元素（本例中为**a**）的内容
* **％ARR(<)**  
    最后定义的数组元素（本例中为**d**）的内容
* **％ARR()或％arr(）** 所有以逗号（**a，b，c，d**）分隔的数组元素
* **％ARR(2)或仅％arr2** 索引为2（本例中为**b**） 的元素的内容
* **％ARR(2:4)**  
    索引为2到4（**b，c，d**） 的已定义元素的内容
* **％ARR(:3)**  
    所有定义的索引最大的3个元素（**a，b，c**）
* **％ARR(3:)**  
    所有定义的从索引3开始的元素（**c，d**）
* **％ARR(1:2)**  
    所有定义的索引从1到2的元素（**a，b**）

笔记：

* 数组实际上将始终定义所有元素，因此，例如％ARR(>)将与％ARR(1)相同，％arr(#)将与％ARR(＃<)相同
* 索引说明符本身可以是变量（例如％ARR(1:％MAX)或％ARR(＃？％FINDME)），但**不能是**变量数组

### 创建一个数组

1.  使用`数组设置` `Array Set`:  
    **Array Set, %arr, a b c d**
2.  使用`变量分离` `Variable Split` 一个存在的 (simple) 变量:  
    **Variable Set %arr a b c d**  
    **Variable Split %arr**
3.  用变量设置 `Variable Set`定义特殊的变量值（注：尾部为正数的变量）  
    **Variable Set, %arr3, c**.
4.  使用数组推送 `Array Push` to add an initial element
5.  一些另外的操作也可以创建结果为数组的值 e.g. `List Files`.

### 插入元素

使用操作： `Array Push`

该_填充空间_参数可能需要更多的解释。仅当一个或多个数组元素未定义时才有意义。例如，如果我们有包含**apple**和**banana**的数组元素％arr1和％arr3 ：

* **数组推送％arr1、1，pear**  
    这样％arr1，％arr2和％arr4包含**pear**，**apple**和**banana** 。
* 但是**数组推送％arr2、1，pear，Fill Spaces**  
    使％arr1，％arr2和％arr3包含**pear**，**apple**和**banana**。

### 移除元素

使用`Array Pop`动作。注意之间的差`Array Pop`和`Variable Clear`： `Pop`降低了阵列中元件的数目，而`Clear`仅仅改变元件为未定义。

示例：如果我们有包含**apple**，**pear**和**banana**的数组元素％arr1，％arr2，％arr3 ：

* **变量清理 ％arr2**  
    使％arr1和％arr3包含**apple**和**banana**。
* 但是**数组弹出 ％arr2**  
    留下％arr1和％arr2包含**apple**和**banana**。

### 删除数组

使用操作`Array Clear`

在大多数情况下，您也可以使用**变量清除 ％arr*** 并选中“模式匹配”，但这也会删除名为“％arrTOODEETOO”的变量，因此`Array Clear`更加安全。

### 排序

该操作除其他外，还提供各种排序选项： `Array Process`

### 数组效率

数组旨在在处理高级数据时提供便利，而不是用于处理天文数据。进行数千个数组操作可能会花费几秒钟的时间（尽管主要是由于Tasker在每个操作之间进行的内部管理工作，而不是由于数组操作本身）。

在存储效率方面，它们也毫无希望。您可能不想在数组中存储数万个项目。

> 译者注：本篇简单翻译官方文档  
> [https://tasker.joaoapps.com/userguide/en/variables.html](https://tasker.joaoapps.com/userguide/en/variables.html)

![](https://taskerm.com/wp-content/uploads/2020/07/tasker-round-512.png)