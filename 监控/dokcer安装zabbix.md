# 使用docker安装zabbix

[TOC]

## 简介

Docker是目前较为流行的开源应用容器引擎，基于Go语言并遵从Apache2.0协议开源。

zabbix是一个基于WEB界面的提供分布式系统监视以及网络监视功能的企业级的开源解决方案。

zabbix由zabbix server与可选组件zabbix agent两部门组成。

zabbix server可以通过SNMP，zabbix agent，ping，端口监视等方法提供对远程服务器/网络状态的监视。

zabbix agent需要安装在被监视的目标服务器上，它主要完成对硬件信息或与操作系统有关的内存，CPU等信息的收集。

##  安装环境

| 镜像                               | 版本                        |
| ---------------------------------- | --------------------------- |
| ubantu(宿主机)                     | 18.04.5 LTS (Bionic Beaver) |
| docker                             | 20.10.2                     |
| MySQL（container）                 | 8.0                         |
| zabbix-java-gateway (container)    | alpine-5.4                  |
| zabbix-server-mysql (container)    | alpine-5.4                  |
| zabbix-web-nginx-mysql (container) | alpine-5.4                  |

## 安装步骤

### 使用docker下载镜像

1. 检查docker运行是否正常，看到`Active`即为正常

   ```shell
   ~# systemctl status docker
   ● docker.service - Docker Application Container Engine
      Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
      Active: active (running) since Wed 2021-06-09 13:17:07 CST; 3 weeks 0 days ago
        Docs: https://docs.docker.com
    Main PID: 2108 (dockerd)
       Tasks: 8
      CGroup: /system.slice/docker.service
              └─2108 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
   
   ```
   
2. docker下载mysql的容器镜像

   ```shell
   ~# docker pull mysql:8.0
   8.0: Pulling from library/mysql
   b4d181a07f80: Pull complete
   a462b60610f5: Pull complete
   578fafb77ab8: Pull complete
   524046006037: Pull complete
   d0cbe54c8855: Pull complete
   aa18e05cc46d: Pull complete
   32ca814c833f: Pull complete
   9ecc8abdb7f5: Pull complete
   ad042b682e0f: Pull complete
   71d327c6bb78: Pull complete
   165d1d10a3fa: Pull complete
   2f40c47d0626: Pull complete
   Digest: sha256:52b8406e4c32b8cf0557f1b74517e14c5393aff5cf0384eff62d9e81f4985d4b
   Status: Downloaded newer image for mysql:8.0
   docker.io/library/mysql:8.0
   
   ```

3. docker 下载 zabbix/zabbix-java-gateway:alpine-5.4-latest

   ```shell
   ~# docker pull zabbix/zabbix-java-gateway:alpine-5.4-latest
   alpine-5.4-latest: Pulling from zabbix/zabbix-java-gateway
   540db60ca938: Pull complete
   f84bb590f298: Pull complete
   de5ed48d4371: Pull complete
   062f7bb1cbd4: Pull complete
   afc366541c27: Pull complete
   c29b4e00e47c: Pull complete
   Digest: sha256:f850577a187a9443eb0969793fa14ae4f386c5542204f12c744e2d195b03212a
   Status: Downloaded newer image for zabbix/zabbix-java-gateway:alpine-5.4-latest
   docker.io/zabbix/zabbix-java-gateway:alpine-5.4-latest
   
   ```

4. docker 下载 zabbix/zabbix-server-mysql:alpine-5.4-latest

   ```shell
   ~# docker pull zabbix/zabbix-server-mysql:alpine-5.4-latest
   alpine-5.4-latest: Pulling from zabbix/zabbix-server-mysql
   540db60ca938: Already exists
   00f30e6d0727: Pull complete
   d5842771006f: Pull complete
   5f1085123b4c: Pull complete
   Digest: sha256:3c577178ee0351a44c58eeae8d324a935891ca9424be8370d7dcbca5c0bd4fc8
   Status: Downloaded newer image for zabbix/zabbix-server-mysql:alpine-5.4-latest
   docker.io/zabbix/zabbix-server-mysql:alpine-5.4-latest
   
   ```

   

5. docker 下载 zabbix/zabbix-web-nginx-mysql:alpine-5.4-latest

   ```shell
   ~# docker pull zabbix/zabbix-web-nginx-mysql:alpine-5.4-latest
   alpine-5.4-latest: Pulling from zabbix/zabbix-web-nginx-mysql
   540db60ca938: Already exists
   79d8b66e9af9: Pull complete
   e170e0eb3be2: Pull complete
   e5b3ee9f38c7: Pull complete
   77bb5c503df3: Pull complete
   Digest: sha256:9ce9763b95cc9c61eecfb95aa53035569a340ceb5e896af4560f8e2415e9532b
   Status: Downloaded newer image for zabbix/zabbix-web-nginx-mysql:alpine-5.4-latest
   docker.io/zabbix/zabbix-web-nginx-mysql:alpine-5.4-latest
   
   ```

6.  查看docker 镜像仓库

   ```shell
   ~# docker images
   REPOSITORY                      TAG                 IMAGE ID       CREATED        SIZE
   zabbix/zabbix-java-gateway      alpine-5.4-latest   2552b7f42e42   37 hours ago   84.4MB
   mysql                           8.0                 5c62e459e087   6 days ago     556MB
   zabbix/zabbix-web-nginx-mysql   alpine-5.4-latest   c75fcde05a14   13 days ago    166MB
   zabbix/zabbix-server-mysql      alpine-5.4-latest   856abc12b012   13 days ago    69MB
   
   ```

   

### 启动docker 镜像

> 这里有一个需要注意的地方，按照官方文档的安装步骤，zabbix组件之间是无法链接，需要修改host文件，将主机名解析为对应dockers容器的ip地址才可以互相连接。
>
> 并且mysql不能安装官方文档的dockers启动命令启动，否则会出现Exit(1)的错误，导致MySQL无法启动。

#### 启动MySQL的实例

输入命令如下：

```shell
 docker run --name mysql-server -t \
      -e MYSQL_DATABASE="zabbix" \
      -e MYSQL_USER="zabbix" \
      -e MYSQL_PASSWORD="zabbix_pwd" \
      -e MYSQL_ROOT_PASSWORD="root_pwd" \
      -d mysql:8.0 \
      --restart unless-stopped \
      --character-set-server=utf8 --collation-server=utf8_bin \
      --default-authentication-plugin=mysql_native_password
```

通过查看docker 实例可以发现，mysql的实例并没有启动成功，出现`Exited(1)`的报错：

```shell
:~# docker ps -a
CONTAINER ID   IMAGE       COMMAND                  CREATED         STATUS                     PORTS     NAMES
19525cb6c62d   mysql:8.0   "docker-entrypoint.s…"   8 seconds ago   Exited (1) 2 seconds ago             mysql-server

```

通过查看dockers的日志发现，其不支持`--restart`的参数:

```shell
~# docker logs 19525cb6c62d
2021-06-30 06:21:37+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.25-1debian10 started.
2021-06-30 06:21:37+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2021-06-30 06:21:37+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.25-1debian10 started.
2021-06-30 06:21:38+00:00 [Note] [Entrypoint]: Initializing database files
2021-06-30T06:21:38.038293Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.0.25) initializing of server in progress as process 41
2021-06-30T06:21:38.039259Z 0 [Warning] [MY-013242] [Server] --character-set-server: 'utf8' is currently an alias for the character set UTF8MB3, but will be an alias for UTF8MB4 in a future release. Please consider using UTF8MB4 in order to be unambiguous.
2021-06-30T06:21:38.039264Z 0 [Warning] [MY-013244] [Server] --collation-server: 'utf8_bin' is a collation of the deprecated character set UTF8MB3. Please consider using UTF8MB4 with an appropriate collation instead.
2021-06-30T06:21:38.045660Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
2021-06-30T06:21:39.209774Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
2021-06-30T06:21:41.413061Z 0 [ERROR] [MY-000068] [Server] unknown option '--restart'.
2021-06-30T06:21:41.413878Z 0 [ERROR] [MY-013236] [Server] The designated data directory /var/lib/mysql/ is unusable. You can remove all files that the server added to it.
2021-06-30T06:21:41.415023Z 0 [ERROR] [MY-010119] [Server] Aborting
2021-06-30T06:21:43.161174Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.0.25)  MySQL Community Server - GPL.

```

去掉参数后即可正常启动：

```shell
~#  docker run --name mysql-server -t \
>       -e MYSQL_DATABASE="zabbix" \
>       -e MYSQL_USER="zabbix" \
>       -e MYSQL_PASSWORD="zabbix_pwd" \
>       -e MYSQL_ROOT_PASSWORD="root_pwd" \
>       -d mysql:8.0 \
>       --character-set-server=utf8 --collation-server=utf8_bin \
>       --default-authentication-plugin=mysql_native_password
b5379518d1a28ba025cdb1b00c2cc6b07a528d038a1a36aff557ccb92b131fe5
~# docker ps -a
CONTAINER ID   IMAGE       COMMAND                  CREATED         STATUS         PORTS                 NAMES
b5379518d1a2   mysql:8.0   "docker-entrypoint.s…"   4 seconds ago   Up 4 seconds   3306/tcp, 33060/tcp   mysql-server

```



#### 启动zabbix-java-gateway

> 这里开始需要使docker实例的hosts文件调用宿主机的hosts文件`-v /etc/hosts:/etc/hosts`，便于容器之间的互联。

```shell
~#   docker run --name zabbix-java-gateway -t \
>   -v /etc/hosts:/etc/hosts \
>       --restart unless-stopped \
>       -d zabbix/zabbix-java-gateway:alpine-5.4-latest
7eda44ca1dee0b3a7fb76c22fa9d217a86c98ad8113f7ffc84a9fe405a993eab
~# docker ps -a
CONTAINER ID   IMAGE                                          COMMAND                  CREATED         STATUS         PORTS                 NAMES
7eda44ca1dee   zabbix/zabbix-java-gateway:alpine-5.4-latest   "docker-entrypoint.s…"   3 seconds ago   Up 3 seconds   10052/tcp             zabbix-java-gateway
b5379518d1a2   mysql:8.0                                      "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   3306/tcp, 33060/tcp   mysql-server

```

#### 启动zabbix-server-mysql

```shell
:~# docker run --name zabbix-server-mysql -t \
>       -v /etc/hosts:/etc/hosts \
>       -e DB_SERVER_HOST="mysql-server" \
>       -e MYSQL_DATABASE="zabbix" \
>       -e MYSQL_USER="zabbix" \
>       -e MYSQL_PASSWORD="zabbix_pwd" \
>       -e MYSQL_ROOT_PASSWORD="root_pwd" \
>       -e ZBX_JAVAGATEWAY="zabbix-java-gateway" \
>       -p 10051:10051 \
>       --restart unless-stopped \
>       -d zabbix/zabbix-server-mysql:alpine-5.4-latest
2127ef69445f3a10d633131e834455384724a9a977b4de752cf73e7888950aae
~# docker ps -a
CONTAINER ID   IMAGE                                          COMMAND                  CREATED         STATUS         PORTS                      NAMES
2127ef69445f   zabbix/zabbix-server-mysql:alpine-5.4-latest   "/sbin/tini -- /usr/…"   5 seconds ago   Up 3 seconds   0.0.0.0:10051->10051/tcp   zabbix-server-mysql
7eda44ca1dee   zabbix/zabbix-java-gateway:alpine-5.4-latest   "docker-entrypoint.s…"   4 minutes ago   Up 4 minutes   10052/tcp                  zabbix-java-gateway
b5379518d1a2   mysql:8.0                                      "docker-entrypoint.s…"   6 minutes ago   Up 6 minutes   3306/tcp, 33060/tcp        mysql-server

```

#### 启动zabbix-web-nginx-mysql

```shell
~# docker run --name zabbix-web-nginx-mysql -t \
>   -v /etc/hosts:/etc/hosts \
>       -e ZBX_SERVER_HOST="zabbix-server-mysql" \
>       -e DB_SERVER_HOST="mysql-server" \
>       -e MYSQL_DATABASE="zabbix" \
>       -e MYSQL_USER="zabbix" \
>       -e MYSQL_PASSWORD="zabbix_pwd" \
>       -e MYSQL_ROOT_PASSWORD="root_pwd" \
>       -p 80:8080 \
>       --restart unless-stopped \
>       -d zabbix/zabbix-web-nginx-mysql:alpine-5.4-latest
8b1eca7732bad510b667b1c7a8f6552c647878f4dd062a580e7ba14ec7683636
~# docker ps -a
CONTAINER ID   IMAGE                                             COMMAND                  CREATED              STATUS              PORTS                            NAMES
8b1eca7732ba   zabbix/zabbix-web-nginx-mysql:alpine-5.4-latest   "docker-entrypoint.sh"   5 seconds ago        Up 4 seconds        8443/tcp, 0.0.0.0:80->8080/tcp   zabbix-web-nginx-mysql
2127ef69445f   zabbix/zabbix-server-mysql:alpine-5.4-latest      "/sbin/tini -- /usr/…"   About a minute ago   Up About a minute   0.0.0.0:10051->10051/tcp         zabbix-server-mysql
7eda44ca1dee   zabbix/zabbix-java-gateway:alpine-5.4-latest      "docker-entrypoint.s…"   5 minutes ago        Up 5 minutes        10052/tcp                        zabbix-java-gateway
b5379518d1a2   mysql:8.0                                         "docker-entrypoint.s…"   8 minutes ago        Up 8 minutes        3306/tcp, 33060/tcp              mysql-server

```

#### 修改宿主机的hosts文件

按照如上操作，目前还无法访问Zabbix的web界面

通过穿docker的日志发现zabbix-server-mysql无法连接上mysql

```shell
~# docker logs 2127ef69445f
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...
**** MySQL server is not available. Waiting 5 seconds...

```

通过如下命令，获取每个docker容器的实际地址

```shell
:~# docker inspect <container>

...
 "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "87ae68c5359126fa156a5cc0fe117cec2aea4631da6463ebb0af27a6c7e0aa4b",
                    "EndpointID": "86c5edb5611d2a394bddb783418258d028b49fb65a00a88116e7135018b9d8e7",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.5",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:05",
                    "DriverOpts": null
                }
...
```

通过如下命令修改宿主机的hosts文件

```shell
vim /etc/hosts


在hosts文件末尾添加如下信息：
172.18.0.5         zabbix-web-nginx-mysql
172.18.0.4         zabbix-server-mysql
172.18.0.3         zabbix-java-gateway
172.18.0.2         mysql-server

```



修改完宿主机后需要重启容器，使得配置生效

```she
docker restart <container>
```



在浏览器输入http://<宿主机IP>

![image-20210630155223255](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630155223255.png)

输入默认账户密码Admin/zabbix,可以看到zabbix的界面。

![image-20210630155536028](http://markdown-bluebaozi.oss-cn-shanghai.aliyuncs.com/img/image-20210630155536028.png)