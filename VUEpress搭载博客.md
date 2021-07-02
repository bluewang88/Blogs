#  vuepress 搭建博客

## 准备环境

### Ubantu环境

安装nodejs和npm包管理器

```shell
apt update
apt intsall -y nodejs npm
```

安装yarn包管理器

```shell
apy intsall -y yarn 
```

创建并进入新的vuepress目录

```shell
mkdir vuepress-starter && cd vuepress-starter
```

使用包管理器进行初始化(这里选择yarn,也可以自己选择npm)

```shell
~/vuepress-starter# yarn init
yarn init v1.22.5
question name (vuepress-starter):
```

在ubantu下安装使用apt直接安装yarn有问题，会有如下报错：

```shell
# yarn init 
-bash: /usr/bin/yarn: No such file or directory
```

需要进行如下操作：

```shel
sudo apt remove cmdtest
sudo apt remove yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn -y
```

或者：

```shel
sudo apt remove cmdtest
sudo apt remove yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn -y
```

在使用`yarn init`就不会报错了

将 VuePress 安装为本地依赖

```shell
```

###  Windows 环境

安装yarn包管理器

https://classic.yarnpkg.com/en/docs/install/#windows-stable

![image-20210702142222007](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210702142222007.png)

安装nodejs

https://nodejs.org/en/download/

![image-20210702144911086](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210702144911086.png)

建议使用`yarn`包管理安装`vuepress`

打开powershell，输入：

```shell
yarn global add vuepress
```

![image-20210702145215884](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210702145215884.png)