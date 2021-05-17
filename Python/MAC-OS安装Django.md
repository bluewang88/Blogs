[TOC]



## 在MacOS中创建虚拟环境

在命令行下输入：

```shell
virtualenv Djangoenv -p python3
```

会有如下输出

```shell
created virtual environment CPython3.9.5.final.0-64 in 456ms
  creator CPython3Posix(dest=/Users/wangwei/Documents/OneDrive/Code项目/PythonProject/ProjetTestVirtualENV/Djangoenv, clear=False, no_vcs_ignore=False, global=False)
  seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/Users/wangwei/Library/Application Support/virtualenv)
    added seed packages: pip==21.1.1, setuptools==56.0.0, wheel==0.36.2
  activators BashActivator,CShellActivator,FishActivator,PowerShellActivator,PythonActivator,XonshActivator
```

如图显示

![image-20210517015404795](/Users/wangwei/Library/Application Support/typora-user-images/image-20210517015404795.png)

同时可以看到在ProjectTestENV文件夹下创建了Djangoenv的文件夹

```shell
 ~/Documents/OneDrive/Code项目/PythonProject/ProjetTestVirtualENV$ ll
total 0
drwxr-xr-x@ 6 wangwei  staff   192B  5 17 01:52 Djangoenv
```

查看该文件夹的结构可以看出是一个包含了一个依赖的bin的独立环境

```shell
 ~/Documents/OneDrive/Code项目/PythonProject/ProjetTestVirtualENV$ tree -L 3
.
└── Djangoenv
    ├── bin
    │   ├── activate
    │   ├── activate.csh
    │   ├── activate.fish
    │   ├── activate.ps1
    │   ├── activate.xsh
    │   ├── activate_this.py
    │   ├── pip
    │   ├── pip-3.9
    │   ├── pip3
    │   ├── pip3.9
    │   ├── python -> /usr/local/opt/python@3.9/bin/python3.9
    │   ├── python3 -> python
    │   ├── python3.9 -> python
    │   ├── wheel
    │   ├── wheel-3.9
    │   ├── wheel3
    │   └── wheel3.9
    ├── lib
    │   └── python3.9
    └── pyvenv.cfg
```

## 激活虚拟环境

在命令行输入如下command：

```shell
source Djangoenv/bin/activate
```

![image-20210517020656037](/Users/wangwei/Library/Application Support/typora-user-images/image-20210517020656037.png)

可以看到我们激活虚拟环境后，输入的所有命令就是在虚拟环境中执行的。这个虚拟环境包含的Python的副本和pip，但我们运行Python命令的时候，就不再是运行原来系统中的python而是这个虚拟环境中的，pip同理。

我们在虚拟环境中使用python3或者pip3时，只需要输入python或者pip即可，因为虚拟环境中只有python3.9的版本二没有python2.x的版本。

## 在虚拟环境中安装Django

```shell
pip install django
#不指定Django的版本，那么默认安装最新的稳定版本
#如果要指定版本输入命令：pip install django==1.11.4
```
Output:
```shell
Collecting django
  Downloading Django-3.2.3-py3-none-any.whl (7.9 MB)
     |████████████████████████████████| 7.9 MB 1.3 MB/s
Collecting asgiref<4,>=3.3.2
  Using cached asgiref-3.3.4-py3-none-any.whl (22 kB)
Collecting sqlparse>=0.2.2
  Using cached sqlparse-0.4.1-py3-none-any.whl (42 kB)
Collecting pytz
  Using cached pytz-2021.1-py2.py3-none-any.whl (510 kB)
Installing collected packages: sqlparse, pytz, asgiref, django
Successfully installed asgiref-3.3.4 django-3.2.3 pytz-2021.1 sqlparse-0.4.1
```
输入如下命令查看Django版本
```shell
django-admin --version
```
Output:
```shell
3.2.2
```

