# Avaya UC&呼叫中心运维指南

## 第1章 Avaya 简介与产品介绍

### 1.1 Avaya公司简介

Avaya源自AT&T和朗讯科技，2009年收购北电（Nortel）的企业网业务。Avaya公司的业务包含了企业IPT部分（IPPBX、IP Office等）、UC的终端产品（X-one系列）、视频产品（redvision）、交换机（Nortel），最有竞争力的是其呼叫中心的全产品线。

### 1.2 Avaya Aura Core 解决方案架构

下图是Avaya Aura解决方案的架构组成，其中心组件是Session Manager负责与各个系统对接。

![image-20210618110305361](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210618110305361.png)

![image-20210530231133451](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/image-20210530231133451.png)

Avaya Aura 解决方案的核心组件如下：

1. Avaya Aura System Manager（SMGR）
2. Avaya Aura Session Manager  （ASM）
3. Avaya  Aura Communication Manager （ACM）
4. Avaya Aura Application Enablement Services （AES）
5. Avaya Aura Media Server （AMS）
6. Presence Services

Avaya联络中心的逻辑架构如下：

![image-20210530222925611](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530222925611.png)

Avaya ACD平台架构

![image-20210530001824144](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530001824144.png)

ACD的主要作用和实现方式

作用：

1. 呼入呼出的路由；
2. 通话排队；
3. 通话分配；
4. 话务流量统计；

实现方式：

1. 硬排队：CM内置的CallCenter的软交换实现排队；
2. 软排队：利用AIC或者CCE等CTI实现排队；

#### Avaya的呼叫处理流程

利用VDBN和Vector脚本实现呼叫流程

![image-20210530003618383](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530003618383.png)



##### 1.2.1 Avaya Cummunication Manager——Avaya的PBX

> ACM是Avaya Aura解决方案中的PBX角色，她负责对呼叫进行处理和路由；
>
> ACM内建了简单的会议和呼叫中心的功能。支持CO（模拟），数字，SIP，H323等协议的trunk；
>
> 支持HA的模式；

语音对网络的性能要求

| Metric                      | Recommended       | Acceptable         |
| --------------------------- | ----------------- | ------------------ |
| One-way Network Delay       | < 80 milliseconds | < 180 milliseconds |
| Network Jitter              | < 10 milliseconds | < 20 milliseconds  |
| Network Packet Loss (Voice) | 1.0%              | 3.0%               |
| Network Packet Loss (Video) | 0.1%              | 0.2%               |
| QoS Enabled                 | Required          | Required           |

###### 1.2.1.1 ACM的硬件服务器

> S8300 属于小型的分支站点的PBX，他不是一个单独硬件服务器，而是作为一个板卡（board），安装在Avaya G700, G450, G430, G350 or G250 Gateway网关上。然后在其上安装ACM服务器。



<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/P0068-1.png" alt="S8300 Server" style="zoom:150%;" />

<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/P0068-2.png" alt="S8300 Server" style="zoom:150%;" />

<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/S8300-lg__59486.1536750192.jpg" alt="S8300 Avaya Icc/lsp C V2 Media Server For G700/ G450/ G350/ G250 (Refurbished)" style="zoom:40%;" />

![image-20210525173658536](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525173658536.png)

![image-20210525173740290](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525173740290.png)



![image-20210525174043598](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525174043598.png)

![image-20210525173844141](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525173939490.png)

![image-20210525174200793](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525174200793.png)

Avaya其他服务器和语音网关的结合的图例：

![image-20210530002149340](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530002149340.png)

##### 1.2.2 Avaya CTI产品-AES（Application Enbalement Server）

AES提供AVAYA 解决方案的一组API接口、协议、和web服务来与其他应用进行对接集成

- 附属交换机应用程序接口 (ASAI)：通过此 API，附属应用程序可以使用Communication Manager功能和服务。与附件的集成通过 API 进行。ASAI 是 Avaya Computer Telephony 的一部分。
- DEFINITY应用程序编程接口 (DAPI)，用于访问Communication Manager 中的控制和数据路径。
- Java 电话应用程序编程接口 (JTAPI)：这是 Avaya Computer Telephony 支持的开放 API，可集成到Communication Manager ASAI。
- 电话应用程序编程接口 (TAPI)：此 API 用于为运行 Microsoft Windows 操作系统的计算机提供电话服务。
- 电话服务应用程序编程接口 (TSAPI)：此开放式 API 受 Avaya Computer Telephony 支持，并可与Communication Manager ASAI集成。

Avaya CTI 产品的位于整体解决方案的位置：

![image-20210530003935637](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530003935637.png)

![Avaya Aura Application Enablement Services (AES)](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/avaya-aura-application-enablement-services-aes-21-638.jpg)

##### 1.2.3 Avaya SBCE（SBCE+EMS）

Avaya SBCE 提供到SIP的UC系统的安全通信。

SBCE包含两个部分：

1. Session Border Controlller；
2. Element Management System(EMS) 一个管理系统；

Avaya SBCE 提供两个版本：

1. 高级版本：
2. 标准版本：

SBC和EMS都能够提供HA的解决方案。

![img](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/GUID-04357C49-5C5A-492F-9A10-69D4DF6FB9F2-low.jpg)

##### 1.2.4 Avaya Aura Media Server (MS)

AMS相当于软件DSP资源，AMS媒体应用服务器支持SIP TLS，SRTP，VoiceXML ，音视频等。

![image-20210618170032933](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210618170032933.png)

![image-20210618170220513](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210618170220513.png)

![Avaya Aura® Media Server](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/P0955-1.jpg)



##### 1.2.5 Avaya Communication Server 1000E

纯IP的IPPBX，支持分布式部署。

2019年不再生产

![Communication Server 1000](https://support.avaya.com/media/product-images/P0714/P0714-1.png)



##### 1.2.6 Avaya Session Manager （ASM）

Avaya的SIP代理服务器/SIP处理服务器，作为Avaya SIP解决方案架构的核心，连接CM，SBC，第三方PBX等应用。ASM服务器主要用于处理SIP呼叫，将其转发到对应的服务器。

ASM的配置需要由SMGR来进行，本身没有web界面。

![image-20210618175232114](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210618175232114.png)



##### 1.2.7 Media Gateway媒体网关

Avaya 提供连接运营商线路的边缘网关设备，如G350、G450等等

![image-20210603135831168](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603135831168.png)

##### 1.2.8 AIC-企业的CTI解决方案

Avaya Interaction Center

* 提供与其他系统对接，如Avaya Call Center Elite等呼叫中心的产品
* 提供坐席客户端（B/S或者C/S）

Avaya Interaction Center（AIC）

Avaya Contact Center Express （CCE）

C/S：Avaya Agent Desktop

![How To Use Avaya Agent for Desktop Tutorial - YouTube](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/hqdefault.jpg)

B/S：Avaya Agent Web Client



##### 1.2.9 AVP(Avaya Voice Portal)-IVR自助服务平台

* 同时支持H323、SIP
* 支持SIP Trunk
* 采用标准的开放接口：VoiceXML ，CCXML，J2EE，MRCP，WebService，等等

Avaya Interactive Response（AIR）

Avaya Voice Portal（AVP）

![image-20210530030133401](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530030133401.png)

##### 1.2.10 CMS (Call Management System)呼叫管理系统（报表系统）

除了提供详细的报表数据，还会提供ACD的管理功能。

BCMR

标准呼叫管理系统

* 由服务器组建和客户端组件构成；
* 运行在WIndows
* C/S

CMS

高级呼叫管理系统

* C/S
* 服务器端运行在SUN  SOLARIS，客户端运行在Windows



* 提供详细的报表

  ![image-20210530022116081](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530022116081.png)

![image-20210530122914249](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530122914249.png)

##### 1.2.11 外呼应用解决方案

软件外呼解决方案

Avaya PDS预测式外拨应用系统

##### 1.2.12 ACD自动呼叫分配系统

基本呼叫中心软件包introductory

精英型呼叫软件包ELIE

智能自动呼叫分配软件包ELITE with advocate

##### 1.2.13 录音系统

对接第三方录音系统，如NICE录音等



##### 1.2.14 WorkFlow Designer 工作流设计工具

用于呼叫中心。



### 1.3 Avaya呼叫中心解决方案的整体架构图

可以从如下的架构图，大概了解Avaya呼叫中心的整体设计和组件。

![image-20210526122702126](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/image-20210526122702126.png)

![image-20210530021142839](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530021142839.png)

![Avaya Aura Contact Center Overview and Specification - PDF Free Download](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/168-0.jpg)

![image-20210530194440175](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530194440175.png)

![image-20210530215435120](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530215435120.png)

#### 1.3.1 呼叫中心处理流程

如图展示了avaya呼叫中心的一通通话处理流程：

![image-20210530225219060](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530225219060.png)



## 第2章 管理Avaya CM

### 2.1 登录管理Communication Manager的方法

##### 2.1.1 SSH 工具登录

> 使用命令行登录Avaya CM的SAT管理程序

命令行输入：

```bash
ssh <user name>@<cm ip> 
```

Output:

```bash
This system is restricted solely to authorized users for legitimate business
purposes only. The actual or attempted unauthorized access, use or modifications
of this system is strictly prohibited. Unauthorized users are subject to
company disciplinary procedures and or criminal and civil penalties under state,
federal or other applicable domestic and foreign laws.

The use of this system may be monitored and recorded for administrative and
security reasons. Anyone accessing this system expressly consents to such
monitoring and recording, and is advised that if it reveals possible evidence
of criminal activity, the evidence of such activity may be provided to law
enforcement officials.

All users must comply with all corporate instructions regarding the protection
of information assets.
Password:   //输入密码
Last login: Tue May 25 18:30:09 CST 2021 from 10.200.15.217 on pts/0
Enter your terminal type (i.e., xterm, vt100, etc.) [vt100]=>
24385: old priority 0, new priority 0

dadmin@SZ-MainServer>
```

这时输入：

```bash
dadmin@SZ-MainServer> sat
```

Output:

```bash
Pin:     //输入Pin码
System: Small                        Software Version: R016x.03.0.124.0

Terminal Type (513, 715, 4410, 4425, VT220, NTT, W2KTT, SUNT): [513]   4410 //4410对应SAT程序
```

最后会显示SAT界面，这时可以输入SAT的相关命令：

```bash
This system is restricted to authorized users for legitimate business purposes.
          Unauthorized access is a criminal violation of the law.
           Copyright 1992 - 2013 Avaya Inc. All Rights Reserved.
Except where expressly stated otherwise, this Product is protected by copyright
and other laws respecting proprietary rights. Certain software programs or
portions thereof included in this Product may contain software distributed
under third party agreements, which may contain terms that expand or limit
rights to use certain portions of the Product. Information identifying third
party components and terms that apply to them are available on Avaya's web
           site at: http://support.avaya.com/ThirdPartyLicense/.

Command:
```







##### 2.1.2 ASA（Avaya Site Administration）登录

ACM有桌面管理软件登陆，进行管理。

Step1：双击打开ASA软件，进入`File->New->Voice System`；

![image-20210628144602673](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628144602673.png)

Step2: 在红框部分输入系统名称，可以是任意名称，只要方便管理员后续识别和操作；

![image-20210628144821637](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628144821637.png)

Step3:选择`Network connection`使用网络连接；

![image-20210628145415849](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628145415849.png)

Step4:在空格处填写ACM的管理地址；

![image-20210628145748104](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628145748104.png)

Step5:保持默认配置，点击下一页；

![image-20210628150119226](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628150119226.png)

Step6:保持默认，点击下一步；

![image-20210628150248466](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628150248466.png)

Step7:保持默认，点击下一步；

![image-20210628150352395](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628150352395.png)

Step8：在红框中输入用户名和密码还有PIN值，输入完成后，点击下一步；

![image-20210628150503657](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628150503657.png)

Step9：检查参数是否正确，并点击`Test`检查是否能够来连接成功；

![image-20210628150733833](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628150733833.png)

Step10：点击完成

![image-20210628150934143](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628150934143.png)

可以使用GEDI的GUI界面

![image-20210527145836760](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527145836760.png)

或者可以使用Emulation（功能全，推荐）

![image-20210628151103529](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210628151103529.png)

##### 2.1.3 WEB登录

1. 在浏览器输入CM的地址，点击continue

   ![image-20210525180221151](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525180221151.png)

2. 输入用户名和密码

   ![image-20210525180319241](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525180319241.png)

看到上次登录信息，点击continue

![image-20210525180448139](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525180448139.png)

3. 进入Administration->Server(Maintenance)

![image-20210525180901221](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525180901221.png)

可以看到管理界面

![image-20210525181034104](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525181034104.png)

### 2.2 常用命令

#### 2.2.1 退出系统

输入`logoff`,看见提示输入`y`，直接退出系统。

![image-20210526153034778](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526153034778.png)

#### 2.2.2 查看时间

输入`display time`:

![image-20210526152517327](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526152517327.png)

输入`set time`设置时间：

![image-20210526152741352](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526152741352.png)

#### 2.2.3 保存配置

##### 2.2.3.1 暂时存储

> avaya cm修改配置后，点击`Enter`键后，并返回`command successful complated`后，会将配置保存在RAM中，断电后会丢失。

##### 2.2.3.2 永久存储

> 输入`save translation`命令，将配置保存到ROM中，过程会花费较长时间，并且在保存配置过程中无法进行配置操作；
>
> avaya同时可以配置计划，定时进行配置保存。输入`display sytem-parameters maintenance`命令可以查看系统的定时备份计划。

![image-20210526151809511](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526151809511.png)

#### 2.2.4 常用动作

```shell
add        新增
change     更改
remove     刪除
list       列表
status     檢視狀態
monitor    監控
```

常用操作对象

```shell
station            分機
agent-loginID      座席工號
hunt-group         尋線組或技能組
trunk-group        中繼組
VDN                虚拟引导号码
vector             虚拟引导脚本
```

命令例子

```shell
Dup station XXX         複製一個與XXX分機配置相同的新號碼
monitor bcms vdn X      監測VDN號“X”的狀況
```

#### 2.2.5 List 命令

```shell
list trunk-group         檢視系統目前的中繼線情況
list hunt-group          檢視系統所設定的尋線組設定
list station             檢視系統所設定的分機
list vdn                 檢視系統設定的虛擬引導號碼
list bcms vdn xxxx       在交換機上檢視VDN xxxx每小時電話接入次數
list bcms skill x        在交換機上檢視尋線組x每小時電話接入次數
List   con   sta         查詢分機（含數字，模擬）板卡port使用狀況
list cti-link            查詢link狀況
List   con   ds1         查詢各DS1板卡port使用狀況
`List   trace   station X 追蹤分機工作狀況（X為分機號碼)`
List   trace   tac   X   追蹤尋線組工作狀況
List   us ext X          有任意一個X的數值串，查詢它在其他地方的使用情況
List   ars ana           檢視此種類型的出局方式(兩種不同的出局方式)
List   aar ana           檢視此種類型的出局方式
自動路由迂迴（aar） — 用於在您自己的專網上路由公司內部的呼叫。
自動路由選擇（ars） — 用於路由您公司進入公網的呼叫。如果您不具有專網， ARS 也用於路由至您公司遠距離辦公地點的呼叫。
List   measurements occupacy last-hour           檢視每三分鐘重新整理的系統話務總量
List   measurements occupacy summary             檢視每一小時重新整理的系統話務總量
List   measurements occupacy summary            檢視間隔時段最忙系統話務總量
List holiday               假日指令碼編寫
List bcms trunk X          檢視X尋線組的話務狀況（bcms即報表系統）
List login                 檢視使用者名稱
List con ca + xx           檢視機櫃板卡用途(機櫃號)
list agent-loginID xxxx    檢視座席工號的設定及狀態
list con ca X              檢視X機櫃上有無port佔用
list test- schedule        檢視測試時間進度表
list agent staffed         檢視所有坐席登入系統狀況，可看到其登入分機等資訊
list skill-status sta      檢視各技能組所對應配置
list ip-interface clan     檢視clan、ip地址，槽位
```

#### 2.2.6 Change 命令

> change 命令对系统有影响，需要谨慎操作。
>
> chang命令操作够厚，不要随意关闭终端视窗，会导致数据丢失，应该输入`logoff`退出

```shell
Change abbreviated-dialing group X  更改尋線組縮略成員
change vector x           更改系統虛擬引導號碼相應的引導路徑
change station xxxx       更改分機引數
change log X              更改（X）使用者的密碼
change ip-services        更改使用者登入埠設定
change node-names ip      更改外接終端IP地址及接入名
change system cdr         記費
change system mu          系統多屏資訊
change isdn public-unknown-N        指定分機送主叫號
change pickup-group X    話務組設定（設定一個通話組，組中成員可做強聽等操作）
change cov path X       “station”設定介面中“coverage path”值即為所要執行的指令碼編號X
change sig X             進入修改信令組頁面
```

#### 2.2.7 monitor 命令

```shell
monitor bcms system           檢視系統各尋線組的執行情況，每一分鐘鍾重新整理一次
monitor bcms skill x          檢視該技能組的詳細登入成員情況，每一分鐘重新整理一次
monitor traffic trunk-group   檢視中繼組的線路佔用情況，每一分鐘重新整理一次
monitor traffic hunt-group    檢視尋線組的線路佔用情況，每一分鐘重新整理一次
monitor bcms vdn X            監測VDN號“X”的狀況
```



### 2.3 拨号计划

> dialplan拨号计划如何处理`被叫号码` ，即当系统内部话机拨号时，所拨打的号码需要在这张表中进行处理，才之后下一步的路由。

#### 2.3.1 查看拨号路由 dialplan

在ASA的命令行输入`display dialplan analysis`

```shell
display dialplan analysis
                             DIAL PLAN ANALYSIS TABLE
                                   Location:  all           Percent Full:    2

       Dialed   Total  Call    Dialed   Total  Call     Dialed   Total  Call
       String   Length Type    String   Length Type     String   Length Type
     0            1    ext    #           3    fac
     1            4    ext    #4          4    dac
     10           4    ext
     17           4    ext
     2            4    ext
     3            4    ext
     4            4    ext
     5            4    ext
     6            4    ext
     7            4    ext
     8            4    ext
     87           4    ext
     88           6    ext
     9            1    fac
     *            3    fac


```

上表中，每三列为一组，每页显示三组。



以第一组第2个为列解释：

```shell
 Dialed   Total  Call   
 String   Length Type 
 1           4    ext 
```

该行表示以`1`开头的四位分机号，例如：

用户拨打`1111`则会匹配到这个路由计划。

输入``display dialplan analysis` 查看系统的拨号方案

![image-20210526154523273](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526154523273.png)

| dialed string                                                | TotalLength        | Calltype                                                     |
| ------------------------------------------------------------ | ------------------ | ------------------------------------------------------------ |
| 拨号的字符串                                                 | 拨号的整个号码长度 | 应该匹配的类型                                               |
| [0-9]                                                        | [1-2]              | attd:定义用户呼叫话务员.如果在fac中启用了attendant access code area,则无法配置attd，只能配置fac |
|                                                              |                    | ext:分机号                                                   |
|                                                              |                    | aar（自动路由迂回）：专网呼叫公司内部路由。使用这个必须激活`ARS/AAR Dialing without FAC`不适用FAC进行ARS和AAR呼叫的系统参数，可以输入`display system-parameters customer-options`查看对应的系统参数是否激活：![image-20210526160335275](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/image-20210526160335275-2016240.png)<br />![image-20210526160416956](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/image-20210526160416956-2017286.png)<br />AAR中的AAR Digit Conversio功能可以进一步做号码转换 |
|                                                              |                    | asr（自动路由选择）：路由到公网的呼叫，ARS中有ARS Digit Conversion可以进一步做好吗转换 |
| 拨号接入码可以是以 1 至 9 的任何数字开始，最多包含四位数字。第一位数字也可以是 * 和 #。 | [1-4]              | fac（功能接入码）：包含了许多功能![image-20210526163602210](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526163602210.png) |
| 拨号接入码可以是以 1 至 9 的任何数字开始，最多包含四位数字。第一位数字也可以是 * 和 #。 | [1-4]              | dac：拨号接入码(包含了中继接入码tac和功能接入码fac)，也就是说上图中#400-#499这100个号码中可以同时匹配tac和fac |

可以使用如下命令修改拨号方案：

输入`change dialplan analysis`

![image-20210701145622016](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210701145622016.png)

##### 2.3.1.1 **DialedString** 

> 匹配被叫号码（将所拨号码从头开始匹配）

##### 2.3.1.2 **Total Length**

> 完整被叫号码的长度

##### 2.3.1.3 **CallType**

> calltype指示下一步路由需要在哪些表中查询（如ars表、aar表等）

###### 2.3.1.3.1 *ext*

分机，在`list station`可以查看所有分机号.这意味着在做内部呼叫。

###### 2.3.1.3.2 *attd*

Attendant Console，只需要拨打一位号码，直接转到话务台。话务员接入码可以是0到9中的任何数字并且仅包含1位或者2位数字。

如果在`FAC（fuature Access Code）`中使用了`Attendant Access Code`字段，那么这里就无法输入`attd`.

######  2.3.1.3.3 *dac*

可以匹配tac+fac

tac（trunk access code）

fac（feature access code）

###### 2.3.1.3.4 FAC 功能接入码

> FAC（feature access code）在FAC处配置完成后，必须在dialplan处配置后才能生效，否则无法使用。

| 名称                                            | 作用                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| Abbreviated Dialing List1 Access Code:          | 缩位拨号列表1接入码                                          |
| Abbreviated Dialing List2 Access Code:          | 缩位拨号列表2接入码                                          |
| Abbreviated Dialing List3 Access Code:          | 缩位拨号列表3接入码                                          |
| Abbreviated Dial - Prgm Group List Access Code: | 缩位拨号 – 程序组列表接入码                                  |
| Announcement Access Code:                       | 录制语音宣告欢迎词的接入                                     |
| Answer Back Access Code:                        | 取回驻留呼叫的功能接入码                                     |
| Attendant Access Code:                          | 呼叫话务台功能代码                                           |
| Auto Alternate Routing (AAR) Access Code:       | 进入专网的功能码                                             |
| Auto Route Selection (ARS) - Access Code 1:     | 进入公网的功能码                                             |
| Automatic Callback Activation:                  | 用于激活/取消自动回叫的功能码                                |
| Call Forwarding Activation Busy/DA: *100  All:  | 激活/取消呼叫转移的功能码                                    |
| Call Forwarding Enhanced Status:    Act:        | 激活/取消呼叫转移增强型的功能码                              |
| Call Park Access Code:                          | 用于设置呼叫驻留的功能码                                     |
| Call Pickup Access Code:                        | 用于设置代接(组群的代接)的功能码                             |
| CAS Remote Hold/Answer Hold-Unhold Access Code: | 用于呼叫保留及远程应答的功能码                               |
| CDR Account Code Access Code:                   | 用于CDR计费标示输入的功能码                                  |
| Change COR Access Code:                         | 用于修改分机COR等级的功能码                                  |
| Change Coverage Access Code:                    | 用于远程修改分机不同涵盖路径的功能码                         |
| Contact Closure  Open Code:                     | 用于关掉或打开一个联络关闭的功能码                           |
| Contact Closure Pulse Code:                     |                                                              |
| Data Origination Access Code:                   | 从语音设备发起一个数据呼叫的功能码                           |
| Data Privacy Access Code:                       | 用于从呼叫等待或其他中断隔离一个数据呼叫                     |
| Directed Call Pickup Access Code:               | 用于指定代接的功能码(功能码+振铃分机号)                      |
| Directed Group Call Pickup Access Code:         | 用于指定组代接的功能码                                       |
| Emergency Access to Attendant Access Code:      | Emergency Access to Attendant 在System-Parameters Customer-Options中为enabled时可用.	用于进入紧急呼叫话务台的功能码 |
| EC500 Self-Administration Access Codes:         | EC500功能自己管理的功能码                                    |
| Enhanced EC500 Activation:                      | 增强型EC500功能激活的功能码                                  |
| Enterprise Mobility User Activation:            | 企业灵活性分机用户激活的功能                                 |
| Extended Call Fwd Activate Busy D/A   All:      | 用于从本地或远程设置某一话机的呼叫前转的功能码               |
| Extended Group Call Pickup Access Code:         | 扩展的组代接功能码                                           |
| Facility Test Calls Access Code:                | 用于测试呼叫的功能码　针对模拟中继                           |
| Flash Access Code:                              | 用于可被中心局交换机识别的中继闪断功能码                     |
| Group Control Restrict Activation:              | 用于更改其它分机COS的功能码,需授权                           |
| Hunt Group Busy Activation:                     | 可将寻线组置忙或解除的功能码                                 |
| ISDN Access Code:                               | 用于呼叫ISDN的功能码而不使用ARS,AAR或UDP                     |
| Last Number Dialed Access Code:                 | 用于重拨最后一个所拔号码的功能码                             |
| Leave Word Calling Message Retrieval Lock:      | 用于锁定信息显示屏的功能码                                   |
| Leave Word Calling Message Retrieval Unlock:    | 用于解除已锁定的信息显示屏的功能码                           |
| Leave Word Calling Send A Message:              | 用于发布一条留言的功能码                                     |
| Leave Word Calling Cancel A Message:            | 用于取消发布一条留言的功能码                                 |
| Limit Number of Concurrent Calls Activation:    | 在一个分机上并发呼叫限制数目功能码                           |
| Malicious Call Trace Activation:                | 用于追踪恶意呼叫的功能码                                     |
| Meet-me Conference Access Code Change:          | Meet-me 会议密码修改功能码                                   |
| PASTE (Display PBX data on Phone) Access Code:  | 用于配合IP坐席，允许一个用户在话机上查看呼叫中心数据的功能码 |
| Personal Station Access (PSA) Associate Code:   | 用于个人分机号码的登陆及登出                                 |
| Per Call CPN Blocking Code Access Code:         | 在一个中继组的CPN封闭是关闭的，当拨这个功能码时，用户可以打开，主叫方的号码不被发送到公网 |
| Per Call CPN Unblocking Code Access Code:       | 在一个中继组的CPN封闭是打开的，当拨这个功能码时，用户可以打开，主叫方的号码可以发送到公网 |
| Posted Messages Activation:                     | 宣布信息激活功能码，需要在System Parameters Customer-Options 中打开 |
| Priority Calling Access Code:                   | 优先权呼叫的功能码                                           |
| Program Access Code:                            | 用于在个人话机上设置缩位拔号的功能码                         |
| Refresh Terminal Parameters Access Code:        | 刷新终端参数的功能码，用于当系统设置改变时在个人话机上更新终端参数 |
| Remote Send All Calls Activation:               | 用于远程激活或解除Send All Calls功能码，需要控制许可         |
| Self Station Display Activation:                | 显示话机本身信息。方法是：输入一个功能代码后，在话机屏幕上显示该分机的号码，姓名、COR、COS、PORT。功能码在Change Feature 内定义.<br />数字话机显示自己的相关信息功能码 例如：分机号码，板卡端口号 |
| Send All Calls Activation:                      | 用于发送所有呼叫的功能码，激活或解除分机将所有来话发送到一个涵盖路径上或者没有信号 |
| Station Firmware Download Access Code:          | 用于分机固件版本下载的功能码，仅2410/2420话机上可以使用      |
| Station Lock Activation:                        | 用于锁定或解锁话机的功能码                                   |
| Station Security Code Change Access Code:       | 用于更改话机安全码的功能码                                   |
| Station User Admin of FBI Assign:               | 用于激活或解除设备繁忙的指示                                 |
| Station User Button Ring Control Access Code:   | 用于控制分机线路键或者桥接键的响铃方式，不响铃或者听得见     |
| Terminal Dial-Up Test Access Code:              | 用于测试数字话机及按键与交换机通讯的功能码                   |
| Terminal Translation Initialization Merge Code: | 启用TTI功能进行分机设置的功能码 ，当系统中的分机为X端口，可以使用此功能码将分机号指定到某一个物理端口上，或将端口上已经分配了的分机号改为X端口 |
| Transfer to Voice Mail Access Code:             | 用于转接到语音信箱的功能码                                   |
| Trunk Answer Any Station Access Code:           | 用于中继应答在任何一个分机上                                 |
| User Control Restrict Activation:               | 用于更改分机约束级别的功能码                                 |
| Voice Coverage Message Retrieval Access Code:   | 允许通过数字显示终端取另一分机信息的功能码                   |
| Voice Principal Message Retrieval Access Code:  | 允许用户通过一个数字显示模块在另一名用户上取回属于自己的语音信息功能码。 |
| Whisper Page Activation Access Code:            | 耳语激活功能码                                               |
| After Call Work Access Code:                    | 进入工作后处理状态时的功能码                                 |
| Assist Access Code:                             | 用于寻求班长坐席帮助的功能码                                 |
| Auto-In Access Code:                            | 进入自动接听电话状态时的功能码                               |
| Aux Work Access Code:                           | 当座席进入非ACD状态时的功能码（例如：小休**）**              |
| Login Access Code:                              | 登陆进入ACD状态（准备）的功能码                              |
| Logout Access Code:                             | 退出ACD状态的功能码                                          |
| Manual-in Access Code:                          | 进入下一ACD任务时所需的功能码                                |
| Service Observing Listen Only Access Code:      | 仅监听某个坐席的功能码                                       |
| Service Observing Listen/Talk Access Code:      | 监听坐席并可以和坐席对话                                     |
| Service Observing No Talk Access Code:          | 监听某个坐席但是不可以对话                                   |
| Add Agent Skill Access Code:                    | 给某个坐席加技能组的功能码                                   |
| Remove Agent Skill Access Code:                 | 删除某个坐席技能的功能码                                     |
| Remote Logout of Agent Access Code:             | 远程退出坐席登录的功能码                                     |

这个和思科的FAC（Force Authzation Code）不是一样的，Cisco 的FAC和Avaya中的Authorization Code保持一致，用户控制终端用户的呼叫权限。

###### 2.3.1.3.5 AAR 自动路由迂回

主要用于系统的内部呼叫。

主要场景有内部分机互拨，内部系统号码等。

使用命令`list aar ana`可以查看系统中的aar分析表：

![image-20210608140920208](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210608140920208.png)

`list aar digit-conversion` 可以查看aar的号码转换

`list aar route-chosen n` `n` 为所拨打的号码

![image-20210608141626553](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210608141626553.png)

###### 2.3.1.3.6 ARS 自动路由选择

ARS（Automatic Route Selection）

ARS是针对出局呼叫选择路由的。ARS通过`ARS Digit Analysis Table`来处理出局的被叫号码，并使用COR和FRL来确定主叫权限。

AAR/ARS的呼叫匹配流程

PBX->dial-plan->AAR/ARS->Route Patten->TRUNK-Group

![image-20210607183652298](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210607183652298.png)

ARS digit analysis table 符合精确匹配原则。

使用命令`disp ars ana xxx` xxx为所拨打的号码，则显示的第一条即为所匹配的路由。

![image-20210607181956737](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210607181956737.png)

在Avaya Call manager中可以下如下列表中查询

![image-20210607184127693](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210607184127693.png)

> 在dial-plan中如果需要使用AAR/ARS功能，那么在系统参数中的`ARS/AAR Dialing without FAC` 参数必须设置为`y`，否则AAR/ARS则需要在FAC中调用。
>
> 使用`display system-parameters customer-options` 来查看参数
>
> ![image-20210608135804975](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210608135804975.png)

###### 2.3.1.3.7 UDP（uniform dialplan）

外部系统与Avaya系统集成，并且这个外部系统的号码从本地avaya系统需要路由过去，则将号码定位为UDP号码。比如

如果avaya系统需要和第三方的系统对接，第三方系统上的号码为7xxx，那么在avaya系统上需要定义7xxx的号码规则为UDP的类型。

#### 2.3.2 寻号规则

> 该小节主要解释avaya的号码路由的匹配流程，并解释路由如何搭配呼叫权限来进行匹配。

##### 2.3.2.1 呼叫权限

###### 2.3.2.1.1 FLR （Fatility Restrict Level ）呼叫能力级别

最重要的一个参数，它定义了一个分机能够使用的路由范围，

只有当COR中的FLR值大于Route Pattern中的FLR值才能够私用该条路由；

FLR分为0-7，数字越大，权限越大。

###### 2.3.2.1.2 COR (Class of Restriction)

> cor用于限制主叫权限.比如定义一个系统用户的呼叫权限，是否可以外呼，就需要对用户的COR进行配置。

查看系统所有cor：

```shell
list cor
```

![image-20210630171600232](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630171600232.png)

查看某个COR的权限信息

```shell
dislplay cor 1
着重关注`FRL`，`Time of Day Chart` 这几个参数
```

![image-20210630171955010](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630171955010.png)

COR中的FRL和Time of Day Chart决定了该COR能够使用的Router pattern

只有当主叫用户的COR中的FRL值大于Router Patten中的FRL值时，该路由才能够被主叫用户匹配到。

Router Pattern中的FRL值如下：

![image-20210630181308095](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630181308095.png)

###### 2.3.2.1.3 COS(Class of Service )

COS定义了一个用户能够访问的功能。COS不适用于trunk-group。

最多可以管理 16 个不同的 COS 编号（0 到 15）。为系统启用租户分区后，您最多可以管理 100 个 COS 组，每个组有 16 个服务等级。

该屏幕列出了每个 COS 或功能组合的默认值。对于特定组合，`y`用于访问该功能，`n`用于拒绝访问。

![image-20210630181607421](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630181607421.png)

![image-20210630181639381](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630181639381.png)

如果系统启用了租户Tenant的概念 (`Tenant partitionig` 参数设置为`y`)

![image-20210630182202083](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630182202083.png)

可以通过如下命令对cos进行修改：

```shell
display cos-group x 查看cos组
change cos-group x  修改cos组
```

如果启用了租户的配置，那么定义一个station的cos的权限需要有station中的TN和COS两个参数来决定

![image-20210630182617434](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630182617434.png)

如果TN是1 ，COS是6 那么应该查看cos-group 1 中的第6列来确定COS的权限。



###### 2.3.2.1.4 partition-router-table

分区路由表用于同意额PBX需要为多个租户路由出局多个TRUNK（即不同租户从自己的中继线路出局）

一般用于ARS表中的下一步路由，如图所示ARS的下一步为`P1`

![image-20210701134601078](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210701134601078.png)

`p1`对应着 `partition-route-table` 中的`Route Index`的`1`（即第一行） 

![image-20210630115500252](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630115500252.png)

下一步则需要确认COR权限中的`Time of Chart`的值是多少，如下图所示的`Time of Chart`值为1，那么确认在`partition-route-table`中`PGN1`（即第一列），最后确定走router pattern `1`

![image-20210701141519558](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210701141519558.png)

> 总结如下：
>
> 1. 在ars表中的 `px` (x为数字)，可以对应partition-route-table 中的`route-index x`;
> 2. cor中的`time of day chart x` 对应 `PGN x`;
> 3. 由上面两个交叉确定了下一步的router-pattern的编号（即为交叉点的数字）；

###### 2.3.2.1.5 路由匹配流程

路由匹配如下图所示：

从终端拨号到找到对应的路由router-pattern

![image-20210701142219545](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210701142219545.png)

router-pattern的匹配逻辑如下：

![image-20210701142431573](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210701142431573.png)

#### 2.3.3 号码规划

> Avaya系统中所有的通话路由都是由号码进行路由的。所以在这几系统之前要做好号码规划，分机号段、trunk号段等等。这里解释介个比较重要的系统路由点。

##### 2.3.3.1 Station 分机

Station用于管理电话（包括模拟话机、数字话机、IP话机、软电话等）；

如果需要修改某一个分机，运行如下命令：

```shell
change station n ,n是station number
```

如果需要添加一个分机则运行如下命令：

```shell
add station n
```



###### 分机类型

<table>
   <tr>
      <td>电话类型</td>
      <td>模型</td>
      <td>作为管理</td>
   </tr>
   <tr>
      <td>单线模拟</td>
      <td>500</td>
      <td>500</td>
   </tr>
   <tr>
      <td></td>
      <td>2500 和 2500 带有消息等待附件</td>
      <td>2500</td>
   </tr>
   <tr>
      <td></td>
      <td>6210</td>
      <td>6210</td>
   </tr>
   <tr>
      <td></td>
      <td>6211</td>
      <td>6210</td>
   </tr>
   <tr>
      <td></td>
      <td>6218</td>
      <td>6218</td>
   </tr>
   <tr>
      <td></td>
      <td>6219</td>
      <td>6218</td>
   </tr>
   <tr>
      <td></td>
      <td>6220</td>
      <td>6220</td>
   </tr>
   <tr>
      <td></td>
      <td>6221</td>
      <td>6220</td>
   </tr>
   <tr>
      <td>来电显示</td>
      <td>带来电显示的模拟电话</td>
      <td>来电显示</td>
   </tr>
   <tr>
      <td></td>
      <td>7101A 和 7102A</td>
      <td>7101A</td>
   </tr>
   <tr>
      <td></td>
      <td>7103A 可编程和原装</td>
      <td>7103A</td>
   </tr>
   <tr>
      <td></td>
      <td>7104A</td>
      <td>7104A</td>
   </tr>
   <tr>
      <td></td>
      <td>8110</td>
      <td>8110</td>
   </tr>
   <tr>
      <td></td>
      <td>DS1FD</td>
      <td>DS1FD</td>
   </tr>
   <tr>
      <td></td>
      <td>7302H、7303H</td>
      <td>7303S</td>
   </tr>
   <tr>
      <td></td>
      <td>带有 C 和 D 音的语音响应单元 (VRU)</td>
      <td>VRU</td>
   </tr>
   <tr>
      <td></td>
      <td>无 C 和 D 音的 VRU</td>
      <td>2500</td>
   </tr>
   <tr>
      <td>单线 DS1/DSO（线路侧 T1/DS1）</td>
      <td>无前向断开的 DS1 设备</td>
      <td>运维</td>
   </tr>
   <tr>
      <td></td>
      <td>带前向断开的 VRU，无 C 和 D 音</td>
      <td>DS1FD 或 DS1SA</td>
   </tr>
   <tr>
      <td></td>
      <td>带前向断开的 VRU，无 C 和 D 音</td>
      <td>VRUFD 或 VRUSA</td>
   </tr>
   <tr>
      <td>终端</td>
      <td>510D</td>
      <td>510</td>
   </tr>
   <tr>
      <td></td>
      <td>515BCT</td>
      <td>515</td>
   </tr>
   <tr>
      <td>多外观混合</td>
      <td>7303S</td>
      <td>7303S、7313H</td>
   </tr>
   <tr>
      <td></td>
      <td>7305H</td>
      <td>7305S</td>
   </tr>
   <tr>
      <td></td>
      <td>7305S</td>
      <td>7305S、7316H、7317H</td>
   </tr>
   <tr>
      <td></td>
      <td>7309H</td>
      <td>7309H、7313H</td>
   </tr>
   <tr>
      <td></td>
      <td>7313H</td>
      <td>7313H</td>
   </tr>
   <tr>
      <td></td>
      <td>7314H</td>
      <td>7314H</td>
   </tr>
   <tr>
      <td></td>
      <td>7315H</td>
      <td>7315H</td>
   </tr>
   <tr>
      <td></td>
      <td>7316H</td>
      <td>7316H</td>
   </tr>
   <tr>
      <td></td>
      <td>7317H</td>
      <td>7317H</td>
   </tr>
   <tr>
      <td>多外观数码</td>
      <td>2402</td>
      <td>2402</td>
   </tr>
   <tr>
      <td></td>
      <td>2410</td>
      <td>2410</td>
   </tr>
   <tr>
      <td></td>
      <td>2420</td>
      <td>2420</td>
   </tr>
   <tr>
      <td></td>
      <td>6402</td>
      <td>6402</td>
   </tr>
   <tr>
      <td></td>
      <td>6402D</td>
      <td>6402D</td>
   </tr>
   <tr>
      <td></td>
      <td>6408</td>
      <td>6408</td>
   </tr>
   <tr>
      <td></td>
      <td>6408+</td>
      <td>6408+</td>
   </tr>
   <tr>
      <td></td>
      <td>6408D</td>
      <td>6408D</td>
   </tr>
   <tr>
      <td></td>
      <td>6408D+</td>
      <td>6408D+</td>
   </tr>
   <tr>
      <td></td>
      <td>6416D+</td>
      <td>6416D+</td>
   </tr>
   <tr>
      <td></td>
      <td>6424D+</td>
      <td>6424D+</td>
   </tr>
   <tr>
      <td></td>
      <td>7401D</td>
      <td>7401D</td>
   </tr>
   <tr>
      <td></td>
      <td>7401+</td>
      <td>7401+</td>
   </tr>
   <tr>
      <td></td>
      <td>7403D</td>
      <td>7403D</td>
   </tr>
   <tr>
      <td></td>
      <td>7404D</td>
      <td>7404D</td>
   </tr>
   <tr>
      <td></td>
      <td>7405D</td>
      <td>7405D</td>
   </tr>
   <tr>
      <td></td>
      <td>7406D</td>
      <td>7406D</td>
   </tr>
   <tr>
      <td></td>
      <td>7406+</td>
      <td>7406+</td>
   </tr>
   <tr>
      <td></td>
      <td>7407D</td>
      <td>7407D</td>
   </tr>
   <tr>
      <td></td>
      <td>7407+</td>
      <td>7407+</td>
   </tr>
   <tr>
      <td></td>
      <td>7410D</td>
      <td>7410D</td>
   </tr>
   <tr>
      <td></td>
      <td>7410+</td>
      <td>7410+</td>
   </tr>
   <tr>
      <td></td>
      <td>7434D</td>
      <td>7434D</td>
   </tr>
   <tr>
      <td></td>
      <td>7444D</td>
      <td>7444D</td>
   </tr>
   <tr>
      <td></td>
      <td>8403B</td>
      <td>8403B</td>
   </tr>
   <tr>
      <td></td>
      <td>8405B</td>
      <td>8405B</td>
   </tr>
   <tr>
      <td></td>
      <td>8405B+</td>
      <td>8405B+</td>
   </tr>
   <tr>
      <td></td>
      <td>8405D</td>
      <td>8405D</td>
   </tr>
   <tr>
      <td></td>
      <td>8405D+</td>
      <td>8405D+</td>
   </tr>
   <tr>
      <td></td>
      <td>8410B</td>
      <td>8410B</td>
   </tr>
   <tr>
      <td></td>
      <td>8410D</td>
      <td>8410D</td>
   </tr>
   <tr>
      <td></td>
      <td>8411B</td>
      <td>8411B</td>
   </tr>
   <tr>
      <td></td>
      <td>8411D</td>
      <td>8411D</td>
   </tr>
   <tr>
      <td></td>
      <td>9408</td>
      <td>9408</td>
   </tr>
   <tr>
      <td></td>
      <td>9404</td>
      <td>9404</td>
   </tr>
   <tr>
      <td></td>
      <td>呼叫大师我</td>
      <td>602A1</td>
   </tr>
   <tr>
      <td></td>
      <td>CALLMASTER II, CALLMASTER III, CALLMASTER IV</td>
      <td>603A1、603D1、603E1、603F1</td>
   </tr>
   <tr>
      <td></td>
      <td>呼叫大师 VI</td>
      <td>606A1</td>
   </tr>
   <tr>
      <td></td>
      <td>IDT1</td>
      <td>7403D</td>
   </tr>
   <tr>
      <td></td>
      <td>IDT2</td>
      <td>7406D</td>
   </tr>
   <tr>
      <td>IP电话</td>
      <td>4601+</td>
      <td>4601+</td>
   </tr>
   <tr>
      <td></td>
      <td>笔记：</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>添加新的 4601 IP 电话时，必须使用 4601+ 分机类型。此站类型启用了自动回叫功能。</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>4602+</td>
      <td>4602+</td>
   </tr>
   <tr>
      <td></td>
      <td>笔记：</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>添加新的 4602 IP 电话时，必须使用 4602+ 分机类型。此站类型启用了自动回叫功能。</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>4606</td>
      <td>4606</td>
   </tr>
   <tr>
      <td></td>
      <td>4610</td>
      <td>4610</td>
   </tr>
   <tr>
      <td></td>
      <td>4612</td>
      <td>4612</td>
   </tr>
   <tr>
      <td></td>
      <td>带有 G3.5 硬件的 4620SW IP</td>
      <td>4620</td>
   </tr>
   <tr>
      <td></td>
      <td>4621</td>
      <td>4621</td>
   </tr>
   <tr>
      <td></td>
      <td>4622</td>
      <td>4622</td>
   </tr>
   <tr>
      <td></td>
      <td>4624</td>
      <td>4624</td>
   </tr>
   <tr>
      <td></td>
      <td>4625</td>
      <td>4625</td>
   </tr>
   <tr>
      <td></td>
      <td>4690</td>
      <td>4690</td>
   </tr>
   <tr>
      <td></td>
      <td>9611</td>
      <td>9611</td>
   </tr>
   <tr>
      <td></td>
      <td>9621</td>
      <td>9621</td>
   </tr>
   <tr>
      <td></td>
      <td>9630</td>
      <td>9630</td>
   </tr>
   <tr>
      <td></td>
      <td>9641</td>
      <td>9641</td>
   </tr>
   <tr>
      <td></td>
      <td>9650</td>
      <td>9650</td>
   </tr>
   <tr>
      <td>SIP IP电话</td>
      <td>4602SIP 带 SIP 固件</td>
      <td>4620SIP</td>
   </tr>
   <tr>
      <td></td>
      <td>4610SIP 带 SIP 固件</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>9608SIPCC</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>9611SIPCC</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>9621SIPCC</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>9641SIPCC</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>4620SIP 带 SIP 固件</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>SIP 软电话或 Avaya one-X Desktop</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>东芝 SP-1020A</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>笔记：</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>任何用于 SIP 网络的带有 SIP 固件的模型电话必须作为 4620SIP、96xxSIP 或 16CC 电话进行管理。</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>笔记：</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>Communication Manager 6.2 版及更高版本不支持 1616SIP CC 和 4620SIP CC 电话。</td>
      <td></td>
   </tr>
   <tr>
      <td></td>
      <td>9601SIP</td>
      <td>9608SIP</td>
   </tr>
   <tr>
      <td></td>
      <td>9620、9630、9630G 9640、9640G 带 SIP 固件</td>
      <td>96xx 或 96xxSIP 电话</td>
   </tr>
   <tr>
      <td></td>
      <td>9608 带 SIP 固件</td>
      <td>—</td>
   </tr>
   <tr>
      <td></td>
      <td>9611 带 SIP 固件</td>
      <td>9611SIP</td>
   </tr>
   <tr>
      <td></td>
      <td>9621 带 SIP 固件</td>
      <td>9621SIP</td>
   </tr>
   <tr>
      <td></td>
      <td>9641 带 SIP 固件</td>
      <td>9641SIP</td>
   </tr>
   <tr>
      <td></td>
      <td>Avaya J129 IP 电话</td>
      <td>J129</td>
   </tr>
   <tr>
      <td></td>
      <td>Avaya J169 IP 电话</td>
      <td>J169</td>
   </tr>
   <tr>
      <td></td>
      <td>Avaya J179 IP 电话</td>
      <td>J179</td>
   </tr>
   <tr>
      <td></td>
      <td>J169CC IP话机</td>
      <td>J169CC</td>
   </tr>
   <tr>
      <td></td>
      <td>J179CC IP电话</td>
      <td>J179CC</td>
   </tr>
   <tr>
      <td>H.323 软电话</td>
      <td>Road Warrior application</td>
      <td>H.323 或 DCP 类型</td>
   </tr>
   <tr>
      <td></td>
      <td>本地 H.323</td>
      <td>H.323</td>
   </tr>
   <tr>
      <td></td>
      <td>单连接</td>
      <td>H.323 或 DCP 类型</td>
   </tr>
   <tr>
      <td></td>
      <td>任何 NI-BRI N1 和 N2 电话</td>
      <td>NI-BRI</td>
   </tr>
   <tr>
      <td></td>
      <td>7505D</td>
      <td>7505D</td>
   </tr>
   <tr>
      <td></td>
      <td>7506D</td>
      <td>7506D</td>
   </tr>
   <tr>
      <td></td>
      <td>7507D</td>
      <td>7507D</td>
   </tr>
   <tr>
      <td></td>
      <td>8503D</td>
      <td>8503D</td>
   </tr>
   <tr>
      <td></td>
      <td>8510T</td>
      <td>8510T</td>
   </tr>
   <tr>
      <td></td>
      <td>8520T</td>
      <td>8520T</td>
   </tr>
   <tr>
      <td>个人电脑</td>
      <td>6300 或 7300</td>
      <td>个人电脑</td>
   </tr>
   <tr>
      <td>语音或数据</td>
      <td>6538 或 6539</td>
      <td>星座</td>
   </tr>
   <tr>
      <td>测试线</td>
      <td>自动取款机</td>
      <td>105TL</td>
   </tr>
   <tr>
      <td>无硬件管理</td>
      <td>—</td>
      <td>XDID 或 XDIDVIP</td>
   </tr>
   <tr>
      <td>按键电话系统界面</td>
      <td>—</td>
      <td>K2500</td>
   </tr>
   <tr>
      <td>无硬件管理</td>
      <td>任何数字集</td>
      <td>—</td>
   </tr>
   <tr>
      <td></td>
      <td>计算机电话集成 (CTI) 站</td>
      <td>CTI</td>
   </tr>
   <tr>
      <td>CTI</td>
      <td>CTI station</td>
      <td>CTI</td>
   </tr>
   <tr>
      <td>XMOBILE</td>
      <td>EC500、DECT 或 PHS</td>
      <td>XMOBILE</td>
   </tr>
   <tr>
      <td>ISDN-BRI 数据模块</td>
      <td>7500</td>
      <td>7500</td>
   </tr>
   <tr>
      <td>承载和信令分离 (SBS) 扩展</td>
      <td>无硬件的 SBS 测试扩展</td>
      <td>SBS</td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>



分机类型举例：

  ***\*2500\** \**模拟分机\****

​    ***\*6408D+\** \**数字分机\****

​    ***\*607A\**** **CallMaster** **V/VI** ***\*专用坐席分机\**** 

​    ***\*ds1fd\** \**IVR\**\**分机（\**\**Line  Side E1\**\**）\****

​    ***\*4606/12/30\** \**IP\**\**电话分机\****

   ***\*asai\** \**CTI\**\**分机\****

| 分机类型 | 标示 |
| -------- | ---- |
| 模拟分机 |      |
| 数字分机 |      |
| IP分机   |      |
| CTI分机  |      |
| IVR分机  |      |
| 坐席分机 |      |

![image-20210603132644864](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603132644864.png)

###### 删除分机号

`remove station <ext>`

###### 添加分机号

`list configuration all`查看板卡端口使用情况

![image-20210701154624192](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210701154624192.png)

`Board Number`槽位号

| 板卡名称         | 作用     |
| ---------------- | -------- |
| ICC MM           |          |
| DS1 MM           |          |
| ANALOG LINE      | 模拟板卡 |
| VAL-ANNOUNCEMENT |          |

##### 2.3.3.2 Trunk

###### 查看TRUNK状态

`status trunk <1-200>`

中继类型

| 中继组类别               | 中继组名称 |
| ------------------------ | ---------- |
| 模拟中继                 |            |
| 数字中继（ISDN PRI/BRI） |            |

中继组类型：

1. CO

市话局 （CO）中继群主要是将你的交换机连接到本地中心局，但也可连接象外部寻呼系统和数据模
块之类的附属设备。

2.DID

直拨内线号 （DID）中继群将呼入直接接通到内部分机，而不经过话务员或其它市话点。

3.ISDN

综合业务数字网（ISDN）中继群允许随呼叫发送话音、数据、视频和信令信息。
ISDN 中继群又分为两种类型：
ISDN- 基本速率接口（ISDN-BRI）中继群，用于将话机、个人计算机和其他桌面设备连接到交换机。
ISDN- 基群速率接口（ISDN-PRI）中继群，用于将设备（例如交换机）连接到网络并且作为设备
（例如交换机和计算机）之间的接口 。

##### 2.3.3.3 Hunt-group

Split(Elit ACD) 豪华版技能组

固定分机作息，bcmsvn-agentID仅仅用于BCMS报表统计

Skill（Delux ACD）精英版技能组

逻辑坐席，可在任意分机上登录，可同时登录多个技能组

一般寻线组---用于IVR



##### 2.3.3.4 VDN&Vector

> VDN虚拟引导号码;
>
> Vector虚拟引导路径（脚本）;



VDN和Vector的作用就是告诉系统如何处理`呼入`的呼叫,一个Vector脚本可以设置最多32个step，来为用户提供个性化的呼叫路由的选择。

每个VDN对应一个Vector，最终由Vector将呼叫路由到对应地方。

![image-20210603142932097](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603142932097.png)



### 2.4 详细场景操作

#### 2.4.1 话机管理

> avaya系统并不是一个纯IP的语音解决方案，所以他的话机类型包含了模拟话机，数字话机，和IP话机。进行话机管理之前需要确认话机的类型从而来确定对应的操作步骤。

##### 2.4.1.1 新增话机的简要操作总结

1. 确定话机型号，模拟的、IP、数字、ISDN、还是混合的；
2. 查找可用的话机端口（`list configuration stations`），未使用端口由符号`u`表示，记录话机端口地址（板卡号+端口号）;
3. 记录端口号与话机分配的分机号；
4. 添加话机`add station xxx` xxx是分机号；
5. Type字段输入话机的型号；
6. port字段输入端口地址，如果是IP电话，则不需要填写Port字段，自动填写为`IP`；
7. Name区域填写类似于`名字+分机号`的内容，内容将会显示在被叫话机上；
8. 如果需要改变某一个话机的某些设置需要，输入`change station xxx`;



添加模拟话机

#### 添加IP话机

##### IP 硬电话

##### IP 软电话

#### 复制话机












#### 2.4.2 Avaya CM 安装补丁

ssh登录CM

```shell
ssh dadmin@10.150.9.10

This system is restricted solely to authorized users for legitimate business
purposes only. The actual or attempted unauthorized access, use or modifications
of this system is strictly prohibited. Unauthorized users are subject to
company disciplinary procedures and or criminal and civil penalties under state,
federal or other applicable domestic and foreign laws.

The use of this system may be monitored and recorded for administrative and
security reasons. Anyone accessing this system expressly consents to such
monitoring and recording, and is advised that if it reveals possible evidence
of criminal activity, the evidence of such activity may be provided to law
enforcement officials.

All users must comply with all corporate instructions regarding the protection
of information assets.
Password:
Last login: Wed Jun  2 14:56:49 CST 2021 from 10.200.14.96 on pts/0
Enter your terminal type (i.e., xterm, vt100, etc.) [vt100]=>
17389: old priority 0, new priority 0

dadmin@SZ-MainServer>
```

avaya底层就是一个linux系统，可以使用linux命令

可以查看自己的当前路径：

```shell
dadmin@SZ-MainServer> pwd
/var/home/dadmin
```

打开`/var/home/ftp/pub`的路径

```bash
dadmin@SZ-MainServer> cd /var/home/ftp/pub
dadmin@SZ-MainServer> pwd
/var/home/ftp/pub
```



查看当前文件夹：

```ba
dadmin@SZ-MainServer> ll
total 5140
-rw-r--r-- 1 dadmin susers 4092623 Jul 20  2017 MST.M
drwxr-xr-x 2 root   root      4096 Mar 20  2013 avaya
-rw-r--r-- 1 root   root   1154357 Apr 23  2020 full_SZ-MainServer_163723_20200423.tar.gz
```

查看可用命令：

```bash
dadmin@SZ-MainServer> dhelp
Stingray Shell Commands

-			    MessageTracer	 acpfindvers
addDenialDesc		    admin_commands	 almcall
almclear		    almdisplay		 almenable
almnotif		    almsnmpconf		 almsummary
almsuppress		    arbmtce		 authtype
autosat			    border_bash		 callpppd
catlog			    cert_cm_postinstall  cert_rsyslog_postinstall
cert_web443_postinstall     cm_plat_ping	 cmpasswd
cmuser			    cmuseradd		 cmuserdel
cmusermod		    corevector		 csrmanage
custalmopt		    defsat		 dhelp
disp_dup_log		    displaydenialevents  dsat
fips_mode		    fullCMrelease	 fwdlreason
gemruleadmin		    getCertRepoData	 getCertUserAlarms
get_lic_sed		    ipsi_qry		 ipsisession
ipsiversion		    issmgrreachable	 licconvert
licextract		    licmigrate		 listhistory
loadcertificate		    loaddisplang	 loadipsi
loadlicense		    loadstbyipsis	 locktrans
logc			    logclear		 logecho
loginreport		    logmst		 logr
logv			    logw		 mo
mta			    mv_lastlog		 mv_status
oldloadipsi		    oldresetipsi	 outage
pingall			    productid		 resetipsi
resetstbyipsis		    restartcause	 rps
rtps			    sat			 satSessions
save_trans		    serialnumber	 server
serverInitialNetworkConfig  setCertRepoData	 settrace
sftp_removal		    sosmlogin		 start
statapp			    statuslicense	 statusserver
stop			    swversion		 systat
telnetenable		    testalarm		 testcustalm
testinads		    testinadsport	 testled
topsting		    txt2xln		 unlocktrans
unused_login_audit	    upd_pe_info		 update_activate
update_commit		    update_deactivate	 update_guard
update_info		    update_remove	 update_show
update_unpack		    vilog		 wlog
wmta			    xln2txt		 xlnrecovery
```

输入update_uppack的命令将补丁文件解压缩

```bash
update_uppack <filename>
```

输入update_activate 安装补丁

```bash
update_activate <filename>
```

卸载补丁

```bash
update_deactivate <filename>
```





## TroubleShooting

### 常用命令

#### list命令

> list 可以查看很多系统配置信息，对系统整体可以有个大概了解 

##### 查看分机号

`list station`

通过GEDI输入如上命令可以看到：

![image-20210527152149922](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527152149922.png)

##### 查看注册分机号

`list registered-ip-sation`

##### 查看板卡

`list configuration all`

端口地址=板卡号+端口号

##### 查看IP接口

`list ip-interface all`

##### 查看呼叫路由

`list route-pattern`

##### 查看TRUNK-Group

`list trunk-group`

##### 查看语音网关

`list media-gateway`

可以查看到CM注册上来的媒体网关，`Reg？`选项表明了该Media Gateway是否已经注册到CM上，并受到CM的管控。

> CM管理媒体网关，类易于思科的MGCP，所有语音配置都在CM上管理配置，网关上没有语音配置，只有基本的网络配置。

![image-20210531153308499](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/image-20210531153308499.png)

##### 查看系统日志

#### display命令

查看系统告警

消除告警

#### 追踪分机号

`list trace station xxx`

#### 追踪trunk

`list trace tac xxx`

#### 查看系统试试中继线路占用情况

`monitor traffic trunk-group`

![image-20210603110913184](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603110913184.png)

#### 查看hunt-group的线路占用情况

`monitor traffic hunt-group`

![image-20210603111116905](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603111116905.png)

#### 查看系统健康状况

`status health`

![image-20210603111546682](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603111546682.png)

#### 查看系统软件许可

`display system-parameters customer-options`

![image-20210603111910360](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603111910360.png)

![image-20210603111929168](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603111929168.png)

![image-20210603111943400](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603111943400.png)

![image-20210603111956593](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603111956593.png)

![image-20210603112018950](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112018950.png)

![image-20210603112032755](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112032755.png)

![image-20210603112043953](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112043953.png)

![image-20210603112055756](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112055756.png)



![image-20210603112107501](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112107501.png)

![image-20210603112122048](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112122048.png)

![image-20210603112137349](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603112137349.png)

#### 查看PBX系统版本

`list configuration software-version`

![image-20210603113117379](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603113117379.png)



### 出现命令`command` havs data locked

* 问题描述：

在命令框中输入`duplicate station xxx` 出现如下报错：

![image-20210527172600244](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527172600244.png)

* 问题分析

  这可能由于管理员在操作命令后，没有正确的退出命令，导致该条命令被lock。

* 解决方案

  1. 需要查看管理员的登录session状况，找到命令lock的管理员

     输入`status logins`可以看到所有管理员的登录状态，并且可以看到管理员当前正在使用的command

     ![image-20210527173802649](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/image-20210527173802649.png)

     图片显示dadmin这个管理员正在使用`stat logins`这个命令。（这是以自己的账号演示，`*`表示这个管理员是你当前登录的管理员）

     2. 输入`reset login-ID 3`将命令被lock的管理员账户重置、登出，从而解决问题。

## 理解Avaya Comunication Manager 功能



## 话机管理



### 使用分机模版新建话机

> 可以通过复制已有的话机新增话机，或者建立话机模版，应用于整个话机组。（只有同型号的话机才能进行复制操作）

1. `list sation`查看所有分机，找到自己需要复制的分机

   ![image-20210527154603922](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527154603922.png)

   或者使用GEDI的GUI页面显示分机，格式更易观看：

   ![image-20210527154948989](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527154948989.png)

2. `display station xxx`,点击`ENTER`,核实是否是需要复制的话机，确认无误后点击`Cancel`；

   ![image-20210527155344586](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527155344586.png)

   ![image-20210527155931162](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527155931162.png)

   ![image-20210527155952828](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527155952828.png)

   ![image-20210527160007535](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527160007535.png)

3. `duplicate station xxx`,点击`ENTER`，建立话机模版；

   ![image-20210527165038286](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527165038286.png)

4. 输入每一部新话机的分机号，端口号，和话机名称；（更具话机类型的不同，创建的模版需要填写的内容不同）

   

### 使用话机类型别名创建话机

有些话机型号在当前版本的CM上没有，但是话机本省可以使用其他型号进行创建注册。

输入`change alias station`创建别名：

![image-20210528125731000](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528125731000.png)

`Alias Set Type`: 填写系统不支持的型号

`Supported Set Type`:填写系统中支持的型号

这种办法可能会导致新型号的话机部分功能无法使用。

### 查看分机号是否是某个组的成员

`list groups-of-extension xxx`

## 功能管理

### 改变功能参数

`display system-parameters feature` 查看系统功能参数

![image-20210528164138514](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528164138514.png)

`change system-parameters feature`

![image-20210528164405207](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528164405207.png)

### 设置短拨号(快速拨号)

`list abbreviated-dialing group xxx `  xxx为group的号码

`add abbrevicated-dialing group next`添加快速拨号组

![image-20210528165904329](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528165904329.png)

`Size`： 快速拨号清单中的号码个数，比如：如果需要添加8个快速拨号的号码，则在这里填写10。

`Program Ext`： 允许填入的分机对快速拨号列表进行修改

> 快速拨号添加号码，最长不超过26位



添加完成快速拨号组之后，需要将其绑定到对应的分机上才能够生效：

![image-20210528165819785](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528165819785.png)



### 设置代答组 pickup

`list pickup-group`

![image-20210528165554005](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528165554005.png)

`add pickup-group next` 一个pickup组最多50个分机号

![image-20210528170814523](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528170814523.png)

#### 定向代答组（directed Call Pickup）



#### 拓展代答组



### 设置呼叫前转

`display system-parameters coverage-forwarding` 查看呼叫前转的参数，设置用户多长时间未应答则进行前转

![image-20210528174904526](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528174904526.png)

![image-20210528174916780](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528174916780.png)

`list call-forwarding`  查看启用了呼叫前转的话机的号码

![image-20210528175614820](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528175614820.png)

#### COS（Class of Service）

COS不能适用于Trunk-group的远程接入功能，COS定义了话机用户本身能够访问的功能；

COS最多分为16个等级（0-15）

COS组最多一百个（系统必须启动分区-Tenant Partition）

查看COS组内的权限功能：

`display cos-group 1`

![image-20210528181441545](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528181441545.png)

![image-20210528181516995](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528181516995.png)

### 建立涵盖路径 coverage path

`coverage path`是指当呼入的呼叫没有应答时，设置这个呼叫按照顺序将呼叫路由到可处理的应答点，如果路由的应答点无法处理，则路由到下一个。应答点可以时分机号也可以是邮箱等。

一个分机最多有6个涵盖点（应答点）

`display coverage path x`

![image-20210528183447990](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528183447990.png)

`add coverage path next` 添加新的涵盖点

![image-20210528183701965](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528183701965.png)

建立完成涵盖点后需要将分机下绑定涵盖路径：

`change station xxx`

![image-20210528183844643](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210528183844643.png)

### 建立增强型涵盖路径 coverage path

### 建立桥接呼叫



## AES 运维管理



Avaya Aura Application Enablement Services(AE Services)是一个用于支撑Avaya Aura Communication Manager(CM)的一个软件平台。AES提供了一个加强的API，协议族和Web服务用以增强CM与应用开发商，第三方软件提供商和系统集成商的合作。

  AES运行在Linux平台上，与CM以及Avaya Contact Center紧密结合。AES提供了一个对已知应用的一个开放平台，同时也是下一代应用程序和商业解决方案的催化剂。

  AES提供以下部署方案：

- 将AES部署在Avaya Aura System Platform上
- 将AES捆绑部署在服务器上。
- 将AES软件单独部署。
- 

AES具有以下服务：

\1. DMCC服务

  Device,Media,and Call Control(DMCC)服务提供了一个第三方的呼叫控制以及自有的呼叫控制（设备控制和媒体控制）。DMCC SDK提供了Java,XML,.NET API。

  DMCC自有呼叫控制：

- 具有设备控制的DMCC提供了配置DMCC软电话,增强支持软电话的CM电话或分机号码的独有或共享控制。DMCC软电话是一个电话或分机的实体，由AES创建并注册在CM上。

- 具有媒体控制的DMCC提供了将通话录制为WAV格式的能力，也提供了将播放WAV文件的语音通知的能力。媒体会话控制同时也提供了一种客户应用通过RTP发送并接受TTY字符流的能力。应用程序能使用这种功能来部署Voice Carry Over(VCO)。TTY功能只有在客户媒体模式下才能使用。

  DMCC第三方媒体控制：

- 具有呼叫控制服务的DMCC使用TSAPI服务来提供一个支持扩展的第三方呼叫控制的能力，比如停留呼叫，创建会议呼叫，改变呼叫，重新连接呼叫及监控呼叫控制事件等。

  

  路由服务：

- 路由服务允许应用请求和接收通话的路由指令。这些由客户路由服务器应用程序发出指令，基于CM提供的入呼叫信息。

\2. TSAPI服务

  Telephony Services API(TSAPI)是一个基于C/C++的提供一个完整的第三方的呼叫控制，如控制特定呼叫或分机，完成路由或入呼叫，接收事件提示，引起CM特征和查询CM信息的API。Java Telephony API(JTAPI)是TSAPI的一个客户侧接口，和TSAPI一样，提供第三方的呼叫控制。

\3. Web服务

  Web服务提供了*比细粒度API更高层次的抽象。Web服务使用Web Service Definition Language(WSDL)和Simple Object Access Protocol(SOAP)连接提供了更加方便通用的接入。*

*4. CVLAN服务*

  *CallVisor LAN服务是一个基于C/C++的API，他用于使能应用程序与AES交换ASAI消息。CVLAN提供了一个全面的第三方呼叫控制能力，如控制特定呼叫或分机，完成入呼叫路由，接收事件消息，引出CM特征和查询CM信息。CVLAN是一个Avaya自有的协议，不用于新的应用程序开发。*

*5. DLG服务*

  *DEFINITY LAN Gateway(DLG)服务通过TCP/IP传送信息。也就是说DLG服务支持CM和AES之间的TCP/IP连接。DLG服务同时也用于传送ASAI/Q.931消息。DLG\*是一个Avaya自有的协议，不用于新的应用程序开发。**

### 查看CTI link的状态

`status aesvcs cti-link`

![image-20210603153603716](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603153603716.png)

## G450 运维

### 登录G450设备

```bash
telnet <IP>
```

查看接口信息

```bash
SZ-G450-001(super)# show ip int b
Showing 3 Interfaces
      Interface             Address     Mask Method        Status
------------------------- --------------- ---- ------ ---------------------
USB-Modem                 10.3.248.253      30 manual      down                 
Vlan 1                    10.150.9.7        24 manual      up                   
Services                  192.11.13.6       30 manual      down   // Service Port在初始化时候连接，子网掩码是30位，所以用电脑连接到网管或者媒体服务器的ServicePort，要手动设置电脑IP位192.11.13.5/30
```



查看系统信息

```bash
SZ-G450-001(super)# show system
System Name             :
System Location         :
System Contact          :
Uptime (d,h:m:s)        : 35,08:27:37
Call Controller Time    : 16:49:45 02 JUN 2021
Serial No               : 12TG41070194
Model                   : G450
HW Ready for FIPS       : No
Chassis HW Vintage      : 1
Chassis HW Suffix       : A
Mainboard HW Vintage    : 2
Mainboard HW Suffix     : B
Mainboard FW Vintage    : 36.8.0
LAN MAC Address         : cc:f9:54:26:a3:a0
WAN1 MAC Address        : cc:f9:54:26:a3:a1
WAN2 MAC Address        : cc:f9:54:26:a3:a2
SERVICES MAC address    : cc:f9:54:26:a3:a3
Memory #1               : 256MB
Memory #2               : Not present
Compact Flash Memory    : No CompactFlash card is installed
PSU #1                  : 400W
PSU #2                  : Not present
Media Socket #1         : MP80 VoIP DSP Module
Media Socket #2         : MP160 VoIP DSP Module
Media Socket #3         : MP80 VoIP DSP Module
Media Socket #4         : Not present
FAN Tray                : Present
```

查看G450媒体网关挂接的服务器

```bash
输入set mgc list ipaddress <CM ip address>将语音网关挂载到CM服务器
SZ-G450-001(super)# show mgc list

PRIMARY MGC HOST, Primary Search Time : 1 min(s)
IPv4 Address         IPv6 Address
-------------------- ----------------------------------------------
10.150.9.10          -- Not Available --

SECONDARY MGC HOST
IPv4 Address         IPv6 Address
-------------------- ----------------------------------------------
10.101.100.10        -- Not Available --
-- Not Available --  -- Not Available --
-- Not Available --  -- Not Available --

sls disabled
```

显示这台G450的网管挂载在两台服务器之下

这时使用ASA连接服务器输入：

`add media-gateway x` x为网关编号，可以任意

`list media-gateway` 可以看到媒体网关是否挂载成功(Num 1 几位该台，并且Reg列显示`y`为注册成功)

![image-20210602170410005](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210602170410005.png)

![image-20210602170424355](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210602170424355.png)

### 升级G450板卡的固件

查看语音网关插槽信息：

```bash
SZ-G450-001(super)# show mg list_config
SLOT   TYPE         CODE        SUFFIX  HW VINTAGE  FW VINTAGE
----   --------     ----------  ------  ----------  -----------
v1     S8300        ICC         D       5           1
v2     E1T1         MM710       B       16          53
v3     E1T1         MM710       B       16          53
v4     E1T1         MM710       B       16          53
v5     -- Not Installed --
v6     Analog       MM716       A       13          98
v7     Analog       MM716       A       13          98
v8     -- Not Installed --
v10    Mainboard    G450        B       2           36.8.0(A)
```



查看语音网关上的板卡固件：

```bash
SZ-G450-001(super)# sh mm
MEDIA MODULE DESCRIPTION: v1
-------------------------------------------------
Type           : ICC
Description    : ICC Media Module
Serial Number  : UNKNOWN
HW Vintage     : 5
HW Suffix      : D
FW Version     : 1
No. of ports   : 2
Faults         : No Fault Messages


This is an MGC controlled Media Module, check
the MGC for additional status information.


MEDIA MODULE DESCRIPTION: v2
-------------------------------------------------
Type           : MM710
Description    : T1/E1 Media Module
Serial Number  : 14TG19245582
HW Vintage     : 16
HW Suffix      : B
FW Version     : 53
No. of ports   : 1
Faults         : No Fault Messages


This is an MGC controlled Media Module, check
the MGC for additional status information.


MEDIA MODULE DESCRIPTION: v3
-------------------------------------------------
Type           : MM710
Description    : T1/E1 Media Module
Serial Number  : 14TG19245723
HW Vintage     : 16
HW Suffix      : B
FW Version     : 53
No. of ports   : 1
Faults         : No Fault Messages


This is an MGC controlled Media Module, check
the MGC for additional status information.

--type q to quit or space key to continue--


MEDIA MODULE DESCRIPTION: v4
-------------------------------------------------
Type           : MM710
Description    : T1/E1 Media Module
Serial Number  : 14TG19245207
HW Vintage     : 16
HW Suffix      : B
FW Version     : 53
No. of ports   : 1
Faults         : No Fault Messages


This is an MGC controlled Media Module, check
the MGC for additional status information.


MEDIA MODULE DESCRIPTION: v5
-------------------------------------------------
Not Installed

MEDIA MODULE DESCRIPTION: v6

--type q to quit or space key to continue--
-------------------------------------------------
Type           : MM716
Description    : Analog Media Module
Serial Number  : 14TG49684434
HW Vintage     : 13
HW Suffix      : A
FW Version     : 98
No. of ports   : 24
Faults         : No Fault Messages


This is an MGC controlled Media Module, check
the MGC for additional status information.


MEDIA MODULE DESCRIPTION: v7
-------------------------------------------------
Type           : MM716
Description    : Analog Media Module
Serial Number  : 14TG51098022
HW Vintage     : 13
HW Suffix      : A
FW Version     : 98

--type q to quit or space key to continue--
No. of ports   : 24
Faults         : No Fault Messages


This is an MGC controlled Media Module, check
the MGC for additional status information.


MEDIA MODULE DESCRIPTION: v8
-------------------------------------------------
Not Installed

```

