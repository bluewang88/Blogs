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
yarn global add vuepress  //全局安装vuepress
```

![image-20210702145215884](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210702145215884.png)

创建一个存放vuepress的目录，并进入该目录

```shell
mkdir vuepress-project
cd vuepress-project
```

初始化yarn

```shell
> yarn init
yarn init v1.22.5
question name (vuepress-project):
question version (1.0.0):
question description:
question entry point (index.js):
question repository url:
question author:
question license (MIT):
question private:
success Saved package.json
Done in 5.51s.
```

这时会在文件夹中创建一个package.json的文件

![image-20210702153355104](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210702153355104.png)



如果上面没有进行去哪卷装vuepress，那么可以在这里进行安装

```shell
yarn add -D vuepress
```

![image-20210702154140542](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210702154140542.png)

创建docs文件夹

```shel
mkdir d
```

