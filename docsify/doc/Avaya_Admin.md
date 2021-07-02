

# Avaya UC&呼叫中心运维笔记

## Avaya 简介与产品介绍

### Avaya简介

Avaya源自AT&T和朗讯科技，2009年收购北电（Nortel）的企业网业务。

### Avaya联络中心架构

联络中心 的逻辑架构：

![image-20210530222925611](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530222925611.png)

#### Avaya ACD平台架构

![image-20210530001824144](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530001824144.png)

#### ACD的主要作用和实现方式

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

### Avaya Aura通信整体解决方案简介

![image-20210530231133451](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530231133451.png)

#### Avaya PBX 交换机产品介绍

##### S8300 Media Server

> S8300 属于小型的Media Server，他不是一个单独服务器，而是作为一个板卡（board），安装在Avaya G700, G450, G430, G350 or G250 Gateway网关上。



<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/P0068-1.png" alt="S8300 Server" style="zoom:150%;" />

<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/P0068-2.png" alt="S8300 Server" style="zoom:150%;" />

<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/S8300-lg__59486.1536750192.jpg" alt="S8300 Avaya Icc/lsp C V2 Media Server For G700/ G450/ G350/ G250 (Refurbished)" style="zoom:40%;" />

![image-20210525173658536](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525173658536.png)

![image-20210525173740290](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525173740290.png)



![image-20210525174043598](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525174043598.png)

![image-20210525173844141](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525173939490.png)

![image-20210525174200793](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210525174200793.png)

![image-20210530002149340](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530002149340.png)

#### Avaya CTI产品-AES（Application Enbalement Server）

Avaya CTI 产品的位于整体解决方案的位置：

![image-20210530003935637](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530003935637.png)

#### Avaya SBCE（SBCE+EMS）

Avaya SBCE 提供到SIP的UC系统的安全通信。

SBCE包含两个部分：

1. Session Border Controlller；
2. Element Management System(EMS) 一个管理系统；

Avaya SBCE 提供两个版本：

1. 高级版本：
2. 标准版本：

SBC和EMS提供HA方案。

![img](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/GUID-04357C49-5C5A-492F-9A10-69D4DF6FB9F2-low.jpg)

#### Avaya Communication Server 1000E

纯IP的IPPBX，支持分布式部署。

2019年不再生产

![Communication Server 1000](https://support.avaya.com/media/product-images/P0714/P0714-1.png)

#### Avaya Aura Media Server (MS)

媒体应用服务器支持SIP TLS，SRTP，VoiceXML ，音视频

#### Avaya Communication Manger （CM）

Avaya CM是Avaya Aura解决方案的软件PBX平台

- 附属交换机应用程序接口 (ASAI)：通过此 API，附属应用程序可以使用Communication Manager功能和服务。与附件的集成通过 API 进行。ASAI 是 Avaya Computer Telephony 的一部分。
- DEFINITY应用程序编程接口 (DAPI)，用于访问Communication Manager 中的控制和数据路径。
- Java 电话应用程序编程接口 (JTAPI)：这是 Avaya Computer Telephony 支持的开放 API，可集成到Communication Manager ASAI。
- 电话应用程序编程接口 (TAPI)：此 API 用于为运行 Microsoft Windows 操作系统的计算机提供电话服务。
- 电话服务应用程序编程接口 (TSAPI)：此开放式 API 受 Avaya Computer Telephony 支持，并可与Communication Manager ASAI集成。

语音对网络的性能要求

| Metric                      | Recommended       | Acceptable         |
| --------------------------- | ----------------- | ------------------ |
| One-way Network Delay       | < 80 milliseconds | < 180 milliseconds |
| Network Jitter              | < 10 milliseconds | < 20 milliseconds  |
| Network Packet Loss (Voice) | 1.0%              | 3.0%               |
| Network Packet Loss (Video) | 0.1%              | 0.2%               |
| QoS Enabled                 | Required          | Required           |

#### G450媒体网关

![image-20210603135831168](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603135831168.png)

#### AIC-企业的CTI解决方案

* 提供与其他系统对接
* 提供坐席客户端（B/S或者C/S）

Avaya Interaction Center（AIC）

Avaya Contact Center Express （CCE）

C/S：Avaya Agent Desktop

![How To Use Avaya Agent for Desktop Tutorial - YouTube](Avaya%E8%BF%90%E7%BB%B4%E7%AC%94%E8%AE%B0.assets/hqdefault.jpg)

B/S：Avaya Agent Web Client



#### AVP(Avaya Voice Portal)-IVR自助服务平台

* 同时支持H323、SIP
* 支持SIP Trunk
* 采用标准的开放接口：VoiceXML ，CCXML，J2EE，MRCP，WebService，等等

Avaya Interactive Response（AIR）

Avaya Voice Portal（AVP）

![image-20210530030133401](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530030133401.png)

#### CMS (Call Management System)呼叫管理系统（报表系统）

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

#### 外呼应用解决方案

软件外呼解决方案

Avaya PDS预测式外拨应用系统

#### ACD自动呼叫分配系统

基本呼叫中心软件包introductory

精英型呼叫软件包ELIE

智能自动呼叫分配软件包ELITE with advocate

#### 录音系统

NICE录音



#### WorkFlow Designer 工作流设计工具



## Avaya呼叫中心解决方案的整体架构

![image-20210530021142839](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530021142839.png)

![Avaya Aura Contact Center Overview and Specification - PDF Free Download](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/168-0.jpg)

![image-20210530194440175](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530194440175.png)

![image-20210530215435120](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530215435120.png)

## 呼叫中心处理流程



![image-20210530225219060](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210530225219060.png)

## Avaya Communication Manager简单系统架构

![image-20210526122702126](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526122702126.png)

## 管理Avaya CM

### 登录S8xxx Server的方法

#### SSH 工具登录

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







#### ASA（Avaya Site Administration）登录

可以使用GEDI的GUI界面

![image-20210527145836760](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527145836760.png)

#### WEB登录

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

#### 退出系统

输入`logoff`,看见提示输入`y`，直接退出系统。

![image-20210526153034778](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526153034778.png)

### 查看时间

输入`display time`:

![image-20210526152517327](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526152517327.png)

输入`set time`设置时间：

![image-20210526152741352](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526152741352.png)

### 保存配置

#### 暂时存储

> avaya cm修改配置后，点击`Enter`键后，并返回`command successful complated`后，会将配置保存在RAM中，断电后会丢失。

#### 永久存储

> 输入`save translation`命令，将配置保存到ROM中，过程会花费较长时间，并且在保存配置过程中无法进行配置操作；
>
> avaya同时可以配置计划，定时进行配置保存。输入`display sytem-parameters maintenance`命令可以查看系统的定时备份计划。

![image-20210526151809511](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210526151809511.png)





### 查看拨号路由 dialplan

**dialedstring** 

**total Length**

**CallType**

*ext*

*attd*

*dac*

*fac*

#### FAC 功能接入码

> FAC（feature access code）在FAC处配置完成后，必须在dialplan处配置后才能生效，否则无法使用

#### AAR

#### ASR



### 查看TRUNK状态

`status trunk <1-200>`

### 分机号Station

分机类型

| Telephone type                                               | Model                                                        | Administered as   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------- |
| Single-line analog                                           | 500                                                          | 500               |
| 2500 and 2500 with Message Waiting Adjunct                   | 2500                                                         |                   |
| 6210                                                         | 6210                                                         |                   |
| 6211                                                         | 6210                                                         |                   |
| 6218                                                         | 6218                                                         |                   |
| 6219                                                         | 6218                                                         |                   |
| 6220                                                         | 6220                                                         |                   |
| 6221                                                         | 6220                                                         |                   |
| CallerID                                                     | Analog telephone with caller ID                              | CallrID           |
| 7101A and 7102A                                              | 7101A                                                        |                   |
| 7103A Programmable and Original                              | 7103A                                                        |                   |
| 7104A                                                        | 7104A                                                        |                   |
| 8110                                                         | 8110                                                         |                   |
| DS1FD                                                        | DS1FD                                                        |                   |
| 7302H, 7303H                                                 | 7303S                                                        |                   |
| Voice Response Unit (VRU) with C and D tones                 | VRU                                                          |                   |
| VRU without C and D tones                                    | 2500                                                         |                   |
| Single-line DS1/DSO (Lineside T1/DS1)                        | DS1 device without forward disconnect                        | OPS               |
| VRU with forward disconnect without C and D tones            | DS1FD or DS1SA                                               |                   |
| VRU with forward disconnect without C and D tones            | VRUFD or VRUSA                                               |                   |
| Terminals                                                    | 510D                                                         | 510               |
| 515BCT                                                       | 515                                                          |                   |
| Multi-appearance hybrid                                      | 7303S                                                        | 7303S, 7313H      |
| 7305H                                                        | 7305S                                                        |                   |
| 7305S                                                        | 7305S, 7316H, 7317H                                          |                   |
| 7309H                                                        | 7309H, 7313H                                                 |                   |
| 7313H                                                        | 7313H                                                        |                   |
| 7314H                                                        | 7314H                                                        |                   |
| 7315H                                                        | 7315H                                                        |                   |
| 7316H                                                        | 7316H                                                        |                   |
| 7317H                                                        | 7317H                                                        |                   |
| Multi-appearance digital                                     | 2402                                                         | 2402              |
| 2410                                                         | 2410                                                         |                   |
| 2420                                                         | 2420                                                         |                   |
| 6402                                                         | 6402                                                         |                   |
| 6402D                                                        | 6402D                                                        |                   |
| 6408                                                         | 6408                                                         |                   |
| 6408+                                                        | 6408+                                                        |                   |
| 6408D                                                        | 6408D                                                        |                   |
| 6408D+                                                       | 6408D+                                                       |                   |
| 6416D+                                                       | 6416D+                                                       |                   |
| 6424D+                                                       | 6424D+                                                       |                   |
| 7401D                                                        | 7401D                                                        |                   |
| 7401+                                                        | 7401+                                                        |                   |
| 7403D                                                        | 7403D                                                        |                   |
| 7404D                                                        | 7404D                                                        |                   |
| 7405D                                                        | 7405D                                                        |                   |
| 7406D                                                        | 7406D                                                        |                   |
| 7406+                                                        | 7406+                                                        |                   |
| 7407D                                                        | 7407D                                                        |                   |
| 7407+                                                        | 7407+                                                        |                   |
| 7410D                                                        | 7410D                                                        |                   |
| 7410+                                                        | 7410+                                                        |                   |
| 7434D                                                        | 7434D                                                        |                   |
| 7444D                                                        | 7444D                                                        |                   |
| 8403B                                                        | 8403B                                                        |                   |
| 8405B                                                        | 8405B                                                        |                   |
| 8405B+                                                       | 8405B+                                                       |                   |
| 8405D                                                        | 8405D                                                        |                   |
| 8405D+                                                       | 8405D+                                                       |                   |
| 8410B                                                        | 8410B                                                        |                   |
| 8410D                                                        | 8410D                                                        |                   |
| 8411B                                                        | 8411B                                                        |                   |
| 8411D                                                        | 8411D                                                        |                   |
| 9408                                                         | 9408                                                         |                   |
| 9404                                                         | 9404                                                         |                   |
| CALLMASTER I                                                 | 602A1                                                        |                   |
| CALLMASTER II, CALLMASTER III, CALLMASTER IV                 | 603A1, 603D1, 603E1, 603F1                                   |                   |
| CALLMASTER VI                                                | 606A1                                                        |                   |
| IDT1                                                         | 7403D                                                        |                   |
| IDT2                                                         | 7406D                                                        |                   |
| IP Telephone                                                 | 4601+Note:When adding a new 4601 IP telephone, you must use the 4601+ station type. This station type has the Automatic Callback feature enabled. | 4601+             |
| 4602+Note:When adding a new 4602 IP telephone, you must use the 4602+ station type. This station type has the Automatic Callback feature enabled. | 4602+                                                        |                   |
| 4606                                                         | 4606                                                         |                   |
| 4610                                                         | 4610                                                         |                   |
| 4612                                                         | 4612                                                         |                   |
| 4620SW IP with G3.5 hardware                                 | 4620                                                         |                   |
| 4621                                                         | 4621                                                         |                   |
| 4622                                                         | 4622                                                         |                   |
| 4624                                                         | 4624                                                         |                   |
| 4625                                                         | 4625                                                         |                   |
| 4690                                                         | 4690                                                         |                   |
| 9611                                                         | 9611                                                         |                   |
| 9621                                                         | 9621                                                         |                   |
| 9630                                                         | 9630                                                         |                   |
| 9641                                                         | 9641                                                         |                   |
| 9650                                                         | 9650                                                         |                   |
| SIP IP Telephone                                             | 4602SIP with SIP firmware4610SIP with SIP firmware9608SIPCC9611SIPCC9621SIPCC9641SIPCC4620SIP with SIP firmwareSIP Softphone or Avaya one-X DesktopToshiba SP-1020ANote:Any model telephone with SIP firmware used for SIP networking must be administered as a 4620SIP, 96xxSIP, or 16CC telephone.Note:Communication Manager Release 6.2 and later do not support 1616SIP CC and 4620SIP CC telephones. | 4620SIP           |
| 9601SIP                                                      | 9608SIP                                                      |                   |
| 9620, 9630, 9630G 9640, 9640G with SIP firmware              | 96xx or 96xxSIP telephone                                    |                   |
| 9608 with SIP firmware                                       | —                                                            |                   |
| 9611 with SIP firmware                                       | 9611SIP                                                      |                   |
| 9621 with SIP firmware                                       | 9621SIP                                                      |                   |
| 9641 with SIP firmware                                       | 9641SIP                                                      |                   |
| Avaya J129 IP Phone                                          | J129                                                         |                   |
| Avaya J169 IP Phone                                          | J169                                                         |                   |
| Avaya J179 IP Phone                                          | J179                                                         |                   |
| J169CC IP Phone                                              | J169CC                                                       |                   |
| J179CC IP Phone                                              | J179CC                                                       |                   |
| H.323 SoftPhone                                              | Road Warrior application                                     | H.323 or DCP type |
| Native H.323                                                 | H.323                                                        |                   |
| Single connect                                               | H.323 or DCP type                                            |                   |
|                                                              | Any NI-BRI N1 and N2 telephone                               | NI-BRI            |
| 7505D                                                        | 7505D                                                        |                   |
| 7506D                                                        | 7506D                                                        |                   |
| 7507D                                                        | 7507D                                                        |                   |
| 8503D                                                        | 8503D                                                        |                   |
| 8510T                                                        | 8510T                                                        |                   |
| 8520T                                                        | 8520T                                                        |                   |
| Personal computer                                            | 6300 or 7300                                                 | Personal computer |
| Voice or data                                                | 6538 or 6539                                                 | Constellation     |
| Test line                                                    | ATMS                                                         | 105TL             |
| Administered without hardware                                | —                                                            | XDID or XDIDVIP   |
| Key telephone system interface                               | —                                                            | K2500             |
| Administered without hardware                                | any digital set                                              | —                 |
| Computer telephony integration (CTI) station                 | CTI                                                          |                   |
| CTI                                                          | CTI station                                                  | CTI               |
| XMOBILE                                                      | EC500, DECT, or PHS                                          | XMOBILE           |
| ISDN-BRI data module                                         | 7500                                                         | 7500              |
| Separation of Bearer and Signaling (SBS) extension           | SBS test extension without hardware                          | SBS               |

| 分机类型        | 标示 |
| ---------------- | -------- |
| 模拟分机 | |
| 数字分机 |   |
| IP分机 | |
| CTI分机 | |
| IVR风机 | |
|坐席分机 | |

![image-20210603132644864](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603132644864.png)

#### 删除分机号

`remove station <ext>`

#### 添加分机号

`list configuration all`查看板卡端口使用情况



`Board Number`槽位号

| 板卡名称         | 作用     |
| ---------------- | -------- |
| ICC MM           |          |
| DS1 MM           |          |
| ANALOG LINE      | 模拟板卡 |
| VAL-ANNOUNCEMENT |          |

#### 添加模拟话机

#### 添加IP话机

##### IP 硬电话

##### IP 软电话

#### 复制话机

###  呼叫权限

#### COR/COS（Class of Restriction/ Class of Service）

COR 定义了PBX中各种对象的呼叫权限和各项功能的使用权限

​	FRL（Firment Restriction Level）当COR中的FRL大于RouterPattern的FRL的值，才能匹配到路由。权限由低到高。

COS定义了服务类型，如话机有无控制台的服务等。



#### VDN/Vector

VDN虚拟引导号码

Vector虚拟引导路径（脚本）

每个VDN对应一个Vector，最终由Vector将呼叫路由到对应地方。

![image-20210603142932097](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210603142932097.png)

### hunt-group

Split(Elit ACD) 豪华版技能组

固定分机作息，bcmsvn-agentID仅仅用于BCMS报表统计

Skill（Delux ACD）精英版技能组

逻辑坐席，可在任意分机上登录，可同时登录多个技能组

一般寻线组---用于IVR

### trunk-group

| 中继组类别               | 中继组名称 |
| ------------------------ | ---------- |
| 模拟中继                 |            |
| 数字中继（ISDN PRI/BRI） |            |



## Avaya CM 安装补丁

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

##### 查看IP接口

`list ip-interface all`

##### 查看呼叫路由

`list route-pattern`

##### 查看TRUNK-Group

`list trunk-group`

##### 查看语音网关

`list media-gateway`

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

### dialplan 拨号方案

#### 查看拨号方案

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

#### 修改拨号方案

输入`change dialplan analysis`

## 话机管理

### 新增话机

1. 确定话机型号，模拟的、IP、数字、ISDN、还是混合的；
2. 查找可用的话机端口（`list configuration stations`），未使用端口由符号`u`表示，记录话机端口地址（板卡号+端口号）;
3. 记录端口号与话机分配的分机号；
4. 添加话机`add station xxx` xxx是分机号；
5. Type字段输入话机的型号；
6. port字段输入端口地址；
7. Name区域填写类似于`名字+分机号`的内容，内容将会显示在被叫话机上；
8. 如果需要改变某一个话机的某些设置需要，输入`change station xxx`;

### 使用分机模版新建话机

> 可以通过复制已有的话机新增话机，或者建立话机模版，应用于整个话机组。（只有同型号的话机才能进行复制操作）

1. `list sation`查看所有分机，找到自己需要复制的分机

   ![image-20210527154603922](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527154603922.png)

   或者使用GEDI的GUI页面显示分机，格式更易观看：

   ![image-20210527154948989](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210527154948989.png)

2. `display station xxx`,点击`ENTER`,核实是否是需要复制的话机，完成后点击`Cancel`；

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



## 出局呼叫路由





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

