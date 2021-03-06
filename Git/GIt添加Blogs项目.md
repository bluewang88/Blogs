[TOC]

# 下载安装Git

1. 一种是通过homebrew安装
2. 一种是通过XCode安装

安装完成后，输入如下commit 查看一条版本
```shell
git --version
```
Output:
```shell
git version 2.24.3 (Apple Git-128)
```
git是分布式版本控制系统，所以每个人都可以提交，需要对提交人标记
配置Git的commit信息，每次commit都会显示该commit由谁修改。
```shell
git config --global user.name "wangwei"
git config --global user.email "bluewangwei88@gmail.com"
```
输入如下命令查看git的全局配置信息：
```shell
git config --list
```
Output:
```shell
credential.helper=osxkeychain
user.name=bluewang88
user.email=bluewangwei88@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
(END)
```

# 创建版本库

版本库又叫仓库（repository），可以理解为是一个目录，git可以管理这个目录下所有的文件

可以在本地创建一个文件夹：
```shell
mkdir Blogs
cd Blogs
```
输入如下命令将这个文件夹改为git管理的仓库（repository）

> 也可以在有文件的目录下输入`git init`，git也会管理目录下所有文件

```shell
git init
```
Output:
```shell
Initialized empty Git repository in /Users/wangwei/Documents/OneDrive/Blogs/.git/
```
这时Blogs目录下会出现`.git`的目录，如果没有则是隐藏目录，输入如下命令查看：
```shell
ll -ah
```
Output:
```shell
total 0
drwxr-xr-x@  3 wangwei  staff    96B  5 17 15:34 .
drwx------@ 26 wangwei  staff   832B  5 17 15:34 ..
drwxr-xr-x@  9 wangwei  staff   288B  5 17 15:34 .git
```
git 只能跟踪文本文件的内容变化，其他文件无法获取内容的变化，只能知道文件大小等属性的变化。
> MicroSoft 的word文档是二进制文件，所以git无法对其内容更改进行跟踪、回溯。

在仓库中创建文本文件：
```shell
vim Readme.md
```
在文件中输入如下Code：
```Markdwon
[TOC]
# 蓝包子的个人学习笔记

这个仓库是作为Blog的前期准备文档，内容比较杂乱，仅供个人参考。
```

# 使用Git在本地仓库管理

> 1. git add \<filename\> 
>  2.  git commit -m "commit massage" 

1. 用命令`git add`告诉git把文件添加到仓库
```shell
git add Readme.md
```
2. 用命令`git commit`告诉git，把文件提交到仓库
```shell
git commit -m "Commit a readme profile"
```
Output:
```shell
[master (root-commit) 5e2f9fa] Commit a readme profile
 1 file changed, 4 insertions(+)
 create mode 100644 Readme.md
```

> 为什么Git添加文件需要add，commit一共两步呢？
> 因为commit可以一次提交很多文件，所以你可以多次add不同的文件，最后一起提交。
> 这一步GIt只能在本地进行版本管理，


# 创建远程仓库GIthub

## 1. 创建密钥对
Github和本地Git通过ssh加密传输的，所以需要在本地有密钥（私钥和公钥）

查看用户根目录下`.ssh`文件夹下有无`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对
> `id_rsa`是私钥
> `id_rsa.pub`是公钥
> 如果文件夹下已经有了这个密钥对，则跳到下一步，否则需要创建密钥对

输入如下命令创建密钥
```shell
ssh-keygen -t rsa -C "youremail@example.com"
```
Output:
```shell
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/wangwei/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/wangwei/.ssh/id_rsa.
Your public key has been saved in /Users/wangwei/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:k44i8EeGcG11Bsgz3cBSWzzbyXSbtiVv+khTQqNbxrw bluewangwei88@gmail.com
The key's randomart image is:
+---[RSA 3072]----+
|   . ===+        |
|   .*.o=+ . .    |
|. . o+.  * ooo   |
| o o    ..+==..  |
|. . o   S ..*=.  |
| o o   o . +.+o  |
|  o o . . . Eo   |
|   o .     ..o   |
|            ...  |
+----[SHA256]-----+
```
> 全部默认回车即可，不需要创建密码
> id_rsa是私钥需要保存好
> id_rsa.pub是公钥可以告诉别人

可以查看用户文件夹下`.ssh`文件夹下是否有`id_rsa`和`id_rsa.pub`这两个文件

```shell
 ~/Documents/OneDrive/Blogs$master$  cd ~/.ssh
 ~/.ssh$ ll
total 72
-rw-------  1 wangwei  staff   2.5K  5 17 17:59 id_rsa
-rw-r--r--  1 wangwei  staff   577B  5 17 17:59 id_rsa.pub
-rw-------  1 wangwei  staff    14K  5 17 04:33 known_hosts
-rw-r--r--  1 wangwei  staff   8.6K  9 29  2020 known_hosts.old
```
## 2. 将本地仓库关联到Github仓库

登录Github
![image-20210517180746522](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517180746522-1246078.png)

打开Github账户设置
<img src="http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517181048603-1246250.png" alt="image-20210517181048603" style="zoom: 33%;" />

在Github上添加生成的公钥
> Github需要解析从本地发到github的内容只需要公钥即可

![image-20210517181338009](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517181338009.png)

将公钥内容复制进去

![image-20210517181620261](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517181620261.png)

![image-20210517181827732](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517181827732-1246709.png)



> Github可以添加多个公钥

在Github上创建项目

![image-20210517182205886](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517182205886-1246927.png)

根据提示可知道github的仓库有两种情况。一种是从github clone到本地，还有一种是将本地已经存在仓库和云端关联，我们这里选择第二种。
![image-20210517182315469](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517182315469-1246999.png)

在本地的`Blogs`仓库下输入如下命令,将本地仓科和云端仓库关联:
```shell
git remote add origin https://github.com/bluewang88/Blogs.git
```
添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

## 3. 将本地仓库内容推送到Github仓库

在本地`Blogs`仓库输入如下命令：

'git c'

```shell
 ~/Documents/OneDrive/Blogs$master$ git branch -M main
 ~/Documents/OneDrive/Blogs$main$ git push -u origin main
Username for 'https://github.com': bluewang88
Password for 'https://bluewang88@github.com':
```
Output:
```shell
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 351 bytes | 175.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/bluewang88/Blogs.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```
> 由于远程库是空的，我们第一次推送`master`分支`main`时，加上了`-u`参数，Git不但会把本地的`main`分支内容推送的远程新的`main`分支，还会把本地的`main`分支和远程的`main`分支关联起来，在以后的推送或者拉取时就可以简化命令。

以后输入如下命令即可推送
```shell
git push origin main
```

![image-20210517183846570](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210517183846570-1247928.png)

## 4. 为命令行Git添加代理

有时运行git push的时候出现报错，则需要为git添加代理，这里本地电脑已经开了VPN代理，所以只需要将其代理改为localhost本机即可。

```shell
fatal: unable to access 'https://github.com/bluewang88/Blogs.git/': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
```
输入命令如下：
```shell
git config --global --add remote.origin.proxy "127.0.0.1:8001"
```



# 当有远端人员push到Github

当一个项目多个人协同工作时，有可能在你push本地仓库到Gihub上时，出现如下报错：

```shell
 ~/Documents/OneDrive/Blogs   main  git push origin main
To https://github.com/bluewang88/Blogs.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/bluewang88/Blogs.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

这时，需要先查看远端的分支情况，输入如下命令：
```shell
git remote
```
Output:
```shell
origin
```
或者：
```shell
git remote -v
```
Output:
```shell
origin	https://github.com/bluewang88/Blogs.git (fetch)
origin	https://github.com/bluewang88/Blogs.git (push)
```

得知远端的分支情况后，将远端的分支同步到本地

```shell
git pull origin main:FETCH_HEAD
```
Output:
```shell
From https://github.com/bluewang88/Blogs
 * [new branch]      main       -> FETCH_HEAD
Already up to date.
```

## git push 出现“fatal: 'origin' does not appear to be a git repository”错误

当正常提交输入如下命令时：
```shell
git push origin main
```
Output:
```shell
error: src refspec main does not match any
error: failed to push some refs to 'origin'
```
或者输入：
```shell
git push origin master
```
Output:
```shell
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

查看远程仓库情况：
```shell
git remote -v
```
output:
```shell
origin
```
解决方案：

输入如下命令添加远程仓库路径：
```shell
git remote add origin https://github.com/bluewang88/Blogs.git
```
再查看远程仓库情况：
```shell
git remote -v
```
output:
```shell
origin	https://github.com/bluewang88/Blogs.git (fetch)
origin	https://github.com/bluewang88/Blogs.git (push)
```



# 总结

本地提交到github步骤
1. `git add .` 添加所有的更新
2. `git commit -m "mesages"` 提交到本地仓库
3. `git push origin main` 推送到github仓库的main分支

## Git 常用命令

```shell
git init                                       #初始化git仓库
git add .                                      #添加当前文件夹下的所有文件
git status                                     #显示状态
git commit                                     #提交代码
git commit  -m ‘注释’                           #提交代码加注释
git log                                        #看提交记录
git push                                       #推送
git push origin master               					 #推送到远程master分支
git push origin ‘版本号’               				 #按照版本号推送到远程
git remote add origin <URL>     							 #关联远程仓库
git tag -a ’版本’ -m ‘描述’         				    #打标签
git push - -tags                       			   #提交到远程
git config --global --list                     #查看git全局配置信息
git config --local --list                      #查看git本地信息
```