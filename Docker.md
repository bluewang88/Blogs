# Ubantu 安装Docker

更新软件包索引

```bash
ubuntu@ip-172-31-37-45:~$ sudo apt-get update
Hit:1 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:3 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Get:4 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [990 kB]
Get:5 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [13.4 kB]
Get:6 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [778 kB]
Get:7 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [167 kB]
Get:8 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [17.5 kB]
Get:9 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Get:10 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [668 kB]
Get:11 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [136 kB]
Get:12 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [7760 B]
Get:13 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [587 kB]
Get:14 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [94.2 kB]
Get:15 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [11.5 kB]
Fetched 3798 kB in 1s (3538 kB/s)
Reading package lists... Done
ubuntu@ip-172-31-37-45:~$
```

安装必要的依赖软件：

```bash
ubuntu@ip-172-31-37-45:~$ sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
Reading package lists... Done
Building dependency tree
Reading state information... Done
ca-certificates is already the newest version (20210119~20.04.1).
ca-certificates set to manually installed.
curl is already the newest version (7.68.0-1ubuntu2.5).
curl set to manually installed.
The following additional packages will be installed:
  python3-software-properties
The following NEW packages will be installed:
  apt-transport-https gnupg-agent
The following packages will be upgraded:
  python3-software-properties software-properties-common
2 upgraded, 2 newly installed, 0 to remove and 29 not upgraded.
Need to get 42.7 kB of archives.
After this operation, 207 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/universe amd64 apt-transport-https all 2.0.5 [1704 B]
Get:2 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/universe amd64 gnupg-agent all 2.2.19-3ubuntu2.1 [5232 B]
Get:3 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/main amd64 software-properties-common all 0.98.9.5 [10.6 kB]
Get:4 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-software-properties all 0.98.9.5 [25.1 kB]
Fetched 42.7 kB in 0s (1823 kB/s)
Selecting previously unselected package apt-transport-https.
(Reading database ... 88004 files and directories currently installed.)
Preparing to unpack .../apt-transport-https_2.0.5_all.deb ...
Unpacking apt-transport-https (2.0.5) ...
Selecting previously unselected package gnupg-agent.
Preparing to unpack .../gnupg-agent_2.2.19-3ubuntu2.1_all.deb ...
Unpacking gnupg-agent (2.2.19-3ubuntu2.1) ...
Preparing to unpack .../software-properties-common_0.98.9.5_all.deb ...
Unpacking software-properties-common (0.98.9.5) over (0.98.9.4) ...
Preparing to unpack .../python3-software-properties_0.98.9.5_all.deb ...
Unpacking python3-software-properties (0.98.9.5) over (0.98.9.4) ...
Setting up apt-transport-https (2.0.5) ...
Setting up python3-software-properties (0.98.9.5) ...
Setting up gnupg-agent (2.2.19-3ubuntu2.1) ...
Setting up software-properties-common (0.98.9.5) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for dbus (1.12.16-2ubuntu2.1) ...
```

使用curl添加源仓库的GPG key:

```bash
ubuntu@ip-172-31-37-45:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
OK
```

将docker的软件源添加到系统：

```bash
ubuntu@ip-172-31-37-45:~$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
Hit:1 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:3 http://us-east-2.ec2.archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu focal-security InRelease
Get:5 https://download.docker.com/linux/ubuntu focal InRelease [41.0 kB]
Get:6 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages [9335 B]
Fetched 50.3 kB in 0s (107 kB/s)
Reading package lists... Done
```

Docker 软件源被启用了，你可以安装软件源中任何可用的 Docker 版本。

1. 安装最新版本的Docker-CE（社区版本）

   ```ba
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```

   

2. 查看dock儿安装的版本：

   ```bash
   ubuntu@ip-172-31-37-45:~$ docker version
   Client: Docker Engine - Community
    Version:           20.10.6
    API version:       1.41
    Go version:        go1.13.15
    Git commit:        370c289
    Built:             Fri Apr  9 22:47:17 2021
    OS/Arch:           linux/amd64
    Context:           default
    Experimental:      true
   Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.24/version: dial unix /var/run/docker.sock: connect: permission denied
   ```

   

3. 查看docker的运行时间：

   ```bash
   ubuntu@ip-172-31-37-45:~$ sudo systemctl status docker
   ● docker.service - Docker Application Container Engine
        Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
        Active: active (running) since Fri 2021-05-28 07:04:07 UTC; 8min ago
   TriggeredBy: ● docker.socket
          Docs: https://docs.docker.com
      Main PID: 35767 (dockerd)
         Tasks: 8
        Memory: 41.8M
        CGroup: /system.slice/docker.service
                └─35767 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
   
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.192473722Z" level=warning msg="Your kernel does not support CPU realtime sch>
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.192489986Z" level=warning msg="Your kernel does not support cgroup blkio wei>
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.192497511Z" level=warning msg="Your kernel does not support cgroup blkio wei>
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.192727603Z" level=info msg="Loading containers: start."
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.359573107Z" level=info msg="Default bridge (docker0) is assigned with an IP >
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.437048965Z" level=info msg="Loading containers: done."
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.520483243Z" level=info msg="Docker daemon" commit=8728dd2 graphdriver(s)=ove>
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.520899804Z" level=info msg="Daemon has completed initialization"
   May 28 07:04:07 ip-172-31-37-45 systemd[1]: Started Docker Application Container Engine.
   May 28 07:04:07 ip-172-31-37-45 dockerd[35767]: time="2021-05-28T07:04:07.575437323Z" level=info msg="API listen on /run/docker.sock"
   ```

   