# OSPF笔记

# 1. OSPF简介

1. OSPF（Open Shortest Path Frist，开放最短路径优先协议），是一种`链路状态`路由协议(Link-state routing Protocol)；

> `距离路由矢量`协议和`链路状态`协议的区别：
>
> 1. 运行距离路由矢量协议（distance-vector routing protocol）的路由器会`周期性`泛洪自己的路由表，即路由更新消息中有路由信息。(链路状态路由协议交换的是链路状态而不是路由信息)；
> 2. 路由器无法知道整网拓扑结构，只能通过路由更新来学习路由这种方式被称为依照传闻更新；（启用链路状态路由协议的每个路由器都能够知道整网的拓扑结构）；

2. OSPF是一个IGP（Interior Gateway Protocol，内部网关协议）协议；

> IGP内部网关协议是指：在一个`自治系统AS`内部所使用的路由协议。

![image-20210617155301338](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210617155301338-1623916389391.png)

3. OSPF使用Dijkstra([戴克斯特拉算法](https://zh.wikipedia.org/wiki/戴克斯特拉算法))的最短路径优先算法SPF；

> Dijkstra算法是采用类似于广度优先的算法解决赋权图的单源最短路径问题，从算法角度简单来说，就将数据结构的`图`中找到最短路径的`树`。

4. OSPFv1用于实验室，OSPFv2广泛用于ipv4（[RFC 2328](https://tools.ietf.org/html/rfc2328)），而OSPFv3则支持了ipv6([RFC 5340](https://tools.ietf.org/html/rfc5340))；

5. OSPF提出区域Area的概念；

> 一个OSPF网络可以由`单一`区域或者`多个`区域组成;
>
> `骨干区域`是一个特殊区域，他和所有其他区域直接相连，任意两个区域之间需要传递路由，必须通过骨干区域；
>
> 如果其他区域不能和骨干区域直接相连，需要创建`virtual link（虚链路）`来创建和骨干区域的虚拟链接；
>
> 每个路由器上同一个区域的`LSDB（链路状态数据库）`是一致的，属于多个区域的路由器会在每个区域独立得维护一份LSDB；

6. OSPF运行在IP协议之上，IP协议号是`89`;

> OSPF不运行在TCP或者UDP协议之上，二十直接承载在IP协议之上

7. OSPF同时使用单播和组播发送Hello包和链路状态更新；

> 组播地址：`224.0.0.5`和`224.0.0.6`

