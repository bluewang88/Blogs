[TOC]
## 启动一个新项目

在虚拟环中中输入如下command：
```shell
django-admin startproject Project1
```
可以看到创建了一个Project的文件夹

![image-20210517022803793](/Users/wangwei/Library/Application Support/typora-user-images/image-20210517022803793.png)

查看Project1文件夹的结构：
```shell
(Djangoenv)  ~/Documents/OneDrive/Code项目/PythonProject/ProjetTestVirtualENV$ tree --matchdirs Project1
Project1     <--存放项目的contain，名字可以任意，
├── Project1 <--Python包名，引用其文件夹下任意文件都需要加上他，如Project1.urls
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```
各个文件的作用：

|   文件名称   |  作用    |
| ---- | ---- |
|  \__init\__.py    |   表明该文件夹是一个Python包   |
|  asgi.py    |      |
|  setting.py    |   和项目有关的所有配置   |
|  urls.py    |  view和路由的mapping    |
|  wsgi.py   |      |
|  manage.py | Django项目的命令行管理工具  |

在Project1文件夹下，输入如下命令启动项目：

```shell
python manage.py runserver
```
Output:
```shell
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
May 16, 2021 - 18:41:33
Django version 3.2.2, using settings 'Project1.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

在浏览器输入：http://127.0.0.1:8000/

![image-20210517024435562](%E5%90%AF%E5%8A%A8Django%E9%A1%B9%E7%9B%AE.assets/image-20210517024435562-1194045.png)

浏览器输入：http://127.0.0.1:8000/admin

![image-20210517024544552](%E5%90%AF%E5%8A%A8Django%E9%A1%B9%E7%9B%AE.assets/image-20210517024544552-1194054.png)

两次WEB访问，命令行会有如下HTTP访问的log输出：

```shell
[16/May/2021 18:43:41] "GET / HTTP/1.1" 200 10697
[16/May/2021 18:43:42] "GET /static/admin/css/fonts.css HTTP/1.1" 304 0
[16/May/2021 18:43:42] "GET /static/admin/fonts/Roboto-Bold-webfont.woff HTTP/1.1" 200 86184
[16/May/2021 18:43:42] "GET /static/admin/fonts/Roboto-Light-webfont.woff HTTP/1.1" 200 85692
[16/May/2021 18:43:42] "GET /static/admin/fonts/Roboto-Regular-webfont.woff HTTP/1.1" 200 85876
[16/May/2021 18:44:00] "GET / HTTP/1.1" 200 10697
[16/May/2021 18:44:00] "GET /static/admin/css/fonts.css HTTP/1.1" 200 423
[16/May/2021 18:44:00] "GET /static/admin/fonts/Roboto-Bold-webfont.woff HTTP/1.1" 200 86184
[16/May/2021 18:44:00] "GET /static/admin/fonts/Roboto-Regular-webfont.woff HTTP/1.1" 200 85876
[16/May/2021 18:44:00] "GET /static/admin/fonts/Roboto-Light-webfont.woff HTTP/1.1" 200 85692
Not Found: /favicon.ico
[16/May/2021 18:44:00] "GET /favicon.ico HTTP/1.1" 404 2112
[16/May/2021 18:45:18] "GET / HTTP/1.1" 200 10697
[16/May/2021 18:45:24] "GET /admin HTTP/1.1" 301 0
[16/May/2021 18:45:24] "GET /admin/ HTTP/1.1" 302 0
[16/May/2021 18:45:25] "GET /admin/login/?next=/admin/ HTTP/1.1" 200 2214
[16/May/2021 18:45:25] "GET /static/admin/css/base.css HTTP/1.1" 200 19513
[16/May/2021 18:45:25] "GET /static/admin/js/nav_sidebar.js HTTP/1.1" 200 1360
[16/May/2021 18:45:25] "GET /static/admin/css/login.css HTTP/1.1" 200 939
[16/May/2021 18:45:25] "GET /static/admin/css/nav_sidebar.css HTTP/1.1" 200 2271
[16/May/2021 18:45:25] "GET /static/admin/css/responsive.css HTTP/1.1" 200 18545
Not Found: /favicon.ico
[16/May/2021 18:45:25] "GET /favicon.ico HTTP/1.1" 404 2112
```
可以使用Ctrl+C终止WEB服务

## 创建一个应用程序

在命令行输入如下command：
```shell
django-admin startapp boards
```
通过这条命令，系统会创建如下目录结构：
```shell
(Djangoenv)  ~/Documents/OneDrive/Code项目/PythonProject/ProjetTestVirtualENV  tree --matchdirs Project1
Project1
├── Project1
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-39.pyc
│   │   ├── settings.cpython-39.pyc
│   │   ├── urls.cpython-39.pyc
│   │   └── wsgi.cpython-39.pyc
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── boards
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── db.sqlite3
└── manage.py
```

boards的文件夹下每个文件的作用如下： 

| \__init__.py |      |
| :---------: | ---- |
| migrations | 在这个文件夹里，Django会存储一些文件以跟踪你在**models.py**文件中创建的变更，用来保持数据库和**models.py**的同步。 |
| admin.py | Django内置应用程序Django admin的配置文件 |
| apps.py | 应用本身的配置文件 |
| modes.py | WEB应用程序的数据实例，modes会呗Django自动转换为数据库表 |
| tests.py | 当前应用程序的的单元测试 |
| views.py | 处理Web应用程序请求(request)/响应(resopnse)周期的文件 |
|             |      |



配置应用程序

修改setting.py的文件，找到`INSTALLED_APPS`变量，修改如下：

```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
# customize app
    'boards',
]
```

 ## 创建view.py文件

 打开boards文件夹下的views.py文件，添加如下代码：
 ```python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.
def home(requets):
    return HttpResponse("Hello World!")
 ```
views.py 视图文件用来响应HTTP requets请求，并返回HTTP Response响应的。

Django在Project1/urls.py 中调用views
```python
from django.contrib import admin
from django.urls import path
from boards import views

urlpatterns = [
    path('', views.home, name='home'),
    path('admin/', admin.site.urls),
]
```
Django使用正则表达式来匹配请求的URL。对于我们的home视图，我使用''正则，它将匹配一个空路径，也就是主页（这个URL：http://127.0.0.1:8000 ）。如果我想匹配的URL是 http://127.0.0.1:8000/homepage/ ，那么我的URL正则表达式就会是：url(r'^homepage/$', views.home, name='home')。

```shell
python manage.py runserver
```

Output:
```shell
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
May 16, 2021 - 19:36:28
Django version 3.2.2, using settings 'Project1.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

浏览器输入http://127.0.0.1:8000

![image-20210517033700254](%E5%90%AF%E5%8A%A8Django%E9%A1%B9%E7%9B%AE.assets/image-20210517033700254.png)

## 总结
1. 创建一个App，后续要在setting.py中注册它；
2. view视图负责响应HTTPRequest（使用HTTPResponse）；
3. view视图创建后需要使用urls.py的path调用它；
4. url负责匹配HTTP requets的url，然后访问不同的视图；



