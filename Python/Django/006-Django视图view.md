[TOC]

# Django的视图view

> 应用文件夹中的views.py是返回网页的HTTP请求内容


## views.py视图函数

Project1/urls.py
·
```python
from django.contrib import admin
from django.urls import path
from boards import views


urlpatterns = [
    path('', views.home, name='home'),
    path('admin/', admin.site.urls),
]
```

board/views.py:

```python
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.


def home(request):
    return HttpResponse("Hello World!")

```

根据线框图需要导入所有的Board板块，即在视图函数中导入Board的mode，并列出所有的Board的主题Topic

![2-2-3.png](https://tva1.sinaimg.cn/large/008i3skNgy1gqscj89xctj30gf0abt9f.jpg)/

可以添加如下的视图函数：

```python
from django.shortcuts import render
from django.http import HttpResponse
from boards.models import Board


# Create your views here.


def home(request):
    boards = Board.objects.all()
    boards_names = list()

    for board in boards:
        boards_names.append(board.name)

    response_html = '<br>'.join(boards_names)

    return HttpResponse(response_html)
```

![image-20210523145602691](https://tva1.sinaimg.cn/large/008i3skNgy1gqsd9xvnb3j316t0u03ze.jpg)

正常情况下我们会使用模版引擎来渲染HTML

# 设置模版引擎

在manage.py的同文件夹下，创建templates文件夹

```shell
tree -L 1
.
├── Project1
├── boards
├── db.sqlite3
├── manage.py
└── templates #创建的文件夹
```

在template中添加如下的html文件：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Board</title>
</head>
<body>
    <h1>Boards</h1>
    {% for board in boards %}
      {{ board.name }} <br>
    {% endfor %}
</body>
</html>
```
`{%...%}`和`{{variable}}`是Django的模版语言

如果需要调用template中的模版文件，需要在setting.py中进行配置调用。

## 调用模版文件

Project1/settings.py 中原始的配置文件如下：
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

需要将`DIRS`这个变量设置为模版文件的路径：

```python
import os

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            os.path.join(BASE_DIR, 'templates')
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

`BASE_DIR`是项目的绝对路径


## 添加视图函数

修改视图函数如下：
```python
from django.shortcuts import render
from django.http import HttpResponse
from .models import Board


def home(request):
    boards = Board.objects.all()

    return render(request, 'home.html', {'boards': boards})
```

![image-20210523171417539](006-Django%E8%A7%86%E5%9B%BEview.assets/image-20210523171417539-1761264.png)

优化的HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Boards</title>
  </head>
  <body>
    <h1>Boards</h1>
    <table border="1">
      <thead>
        <tr>
          <th>Board</th>
          <th>Posts</th>
          <th>Topics</th>
          <th>Last Post</th>
        </tr>
      </thead>
      <tbody>
        {% for board in boards %}
          <tr>
            <td>
              {{ board.name }}<br>
              <small style="color: #888">{{ board.description }}</small>
            </td>
            <td>0</td>
            <td>0</td>
            <td></td>
          </tr>
        {% endfor %}
      </tbody>
    </table>
  </body>
</html>
```

![image-20210523171729651](https://tva1.sinaimg.cn/large/008i3skNgy1gqshcr7x38j31610u0guk.jpg)


