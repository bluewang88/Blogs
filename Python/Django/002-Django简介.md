# Django简介

> Django是由python开发的开源WEB框架
> Django 本身是基于MVC（mode+view+Controller）的设计模式而开发的，但在MVC的基础上使用了MTV（mode+template+view）的设计模式

## MVC和MTV介绍

### MVC

MVC（mode-view-controller）是软件工程中将系统耦合，组织系统的设计模式。
MVC是将业务逻辑与显示界面分离的一种方法，他将软件系用氛围三个部分：
1. mode（模型）：主要负责业务逻辑，并且与数据库交互
2. view（视图）：图形界面，负责与用户交互的界面
3. controller（控制器）： 对请求request进行处理和转发


### MTV

Django自己的

M（model）：负责业务对象和数据库的ORM映射；

T（Template）：负责给客户看的页面

V（View）：负责业务逻辑，在何时展现页面给用户

URL分发器：将不同的URL请求分发给不同的view处理

![img](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/1589777036-2760-fs1oSv4dOWAwC5yW.png)
