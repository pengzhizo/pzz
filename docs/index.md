
docker学习

docker安装

docker命令

​	镜像命令

​	容器命令

​	操作命令

docker镜像

容器数据卷

dockerFile

docker网络原理

IDEA整合Docker

Docker Compose

Docker Swarm

CI\CD jenkins



## Docker概述

docker为什么出现  

一款产品 开发—上线 两套环境、应用配置

开发  运维 

环境配置十分麻烦，每一个机器都要部署环境（xxx）费时费力

发布一个项目（jar+（Redis、 mysql 、jdk、Es）Hodoop），配置超级麻烦，不能跨平台。

windows，最后发布到Linux 

传统 开发jar 运维来做

现在 开发打包部署上线 一套流程完成



java  apk  发布（应用商店） 使用apk 安装即可

java ---jar（环境）---打包项目带上环境（镜像）---（docker仓库 商店）--下载我们发布的 镜像 ---直接运行即可  

docker给以上的问题，提出了解决方案

docker思想来自于集装箱

jre---多个应用（端口冲突）--原来都是交叉的 

隔离：docker核心思想 打包装箱 每个箱子是互相隔离的

Docker 通过隔离机制，可以将服务器利用到极致





## Docker历史、

2010年，几个搞IT年轻人，就在美国成立了一家公司dotCloud

容器化技术

他们将自己技术（容器化技术）匿名就是Docker

为了公司活下去就把代码开源

开源代码

2013年Docker开源

Docker越来越多发现了Docker优点 火了 docker每个月更新一个版本

在2014年4月9号 docker发布

docker为什么怎么火 十分轻巧

在容器技术之前，都是用虚拟技术

虚拟机 vm  笨重  

虚拟机也是虚拟化技术，docker容器化技术，也是一种虚拟化技术

vm linux centos原生镜像（一个电脑）隔离，需要开启多个虚拟机  几个G  几分钟

docker 隔离，镜像（最核心的环境 4m+jdk+mysql）十分的小巧，运行镜像就可以了 小巧  几个M kb 秒级启动

现在所以开发人员都必须会





docker是基于Go语言开发的  开源项目

文档学习 docker的文档是超级详细https://docs.docker.com/

仓库地址https://hub.docker.com/





## docker能干吗

之前虚拟机技术

模拟一台电脑占内存比较大

虚拟化技术缺点

1、占资源比较多

2、沉余步骤多

3、启动极慢

容器化技术

容器化技术它不是模拟的一个完整的操作系统

比较docker 和虚拟机的不同

传统虚拟机，虚拟出一条硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件

容器内的应用直接运行在宿主机的内容，容器是没有自己的内核的，也没有虚拟我们的硬件，所以就轻便了

每个容器间都是相互隔离、每个容器内核都有一个属于自己的文件系统，互不影响

DevOps(开发 运维)

### 应用更快速的交付和部署

传统 一端文档，安装程序

Docker 打包镜像发布测试 ，一建运行

### 便捷的升级和扩容

使用了Docker之后 我们部署应用就和积木一样了

项目打包为了一个镜像，扩展 服务器A 服务器B

### 更简单的系统运维

在容器化之后，我们的开发，测试环境都是极度一致的

### 更高效的计算资源利用

Docker是内核级别的虚拟化，可以在一个物理机上可以运行更多的容器化实例 服务器的性能可以被压榨到极致



## Docker安装

三部分  客服端 服务器 仓库

docker run运行

docker pull拉去

docker build构建容器



镜像（image）

docker镜像就好比是一个模板，可以通过这个模板来创建容器服务， tomcat镜像==run==tomcat01（提供服务）

通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）

容器（container）

docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建的

启动  停止  删除  基本命令

目前就可以把这个容器理解为就是一个简易的linux系统

仓库（repository）

仓库就是存放镜像的地方

仓库分为公有仓库和私有仓库

官方 docker hub

阿里云  都有容器服务



### 安装docker

需要会一点点linux的基础

Centos7

我们使用xshell链接远程服务器进行操作

环境查看

系统内核3.0

查看cent0s7 版本uname -r

```
[root@localhost ~]# cat /etc/os-release 
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

```
[root@localhost ~]# uname -r
3.10.0-693.el7.x86_64

```

安装 看帮助文档

1：较旧的Docker版本称为`docker`或`docker-engine`。如果已安装这些程序，请卸载它们以及相关的依赖项。

```
1卸载旧版本
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
2、安装需要的安装包
  $ sudo yum install -y yum-utils
3、设置镜像仓库
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo 默认国外的
    
$ sudo yum-config-manager \
    --add-repo \
     http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo 阿里云的
     
     
     
4、更新索引
$ yum makecache fast

     
5、安装Docker相关内容docker-ce 社区版 ee企业版
$ sudo yum install docker-ce docker-ce-cli containerd.io

6、启动Docker。

$ sudo systemctl start docker


7、查看启动成功没 和安装成功
[root@localhost ~]# docker version
Client: Docker Engine - Community
 Version:           19.03.12
 API version:       1.40
 Go version:        go1.13.10
 Git commit:        48a66213fe
 Built:             Mon Jun 22 15:46:54 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community  社区版
 Engine:
  Version:          19.03.12
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.10
  Git commit:       48a66213fe
  Built:            Mon Jun 22 15:45:28 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
  
  
 8、hello-world
 $ docker run hello-world
 
 
 9、[root@localhost ~]# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:49a1c8800c94df04e9658809b006fd8a686cab8028d33cfba2cc049724254202
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 
 
10、查看下载hello world 镜像
docker images

  
```

![image-20200722095708538](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722095708538.png)

```
11、卸载docker 

1. 卸载Docker Engine，CLI和Containerd软件包：

   $ sudo yum remove docker-ce docker-ce-cli containerd.io

2. 主机上的映像，容器，卷或自定义配置文件不会自动删除。要删除所有图像，容器和卷：

   $ sudo rm -rf /var/lib/docker
   #/默认安装目录/var/lib/docker

您必须手动删除所有已编辑的配置文件。
```

### 阿里云镜像加速

1、登入阿里云

2、找到容器镜像服务

![image-20200722101054947](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722101054947.png)

4、配置加速器

```
sudo mkdir -p /etc/docker 创建文件
sudo tee /etc/docker/daemon.json <<-'EOF' 
{  "registry-mirrors": ["https://0rcohmfh.mirror.aliyuncs.com"] 
} EOF 配置阿里云
sudo systemctl daemon-reload 重启
sudo systemctl restart docker 启动
```

### 回顾holler world

![image-20200722101908039](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722101908039.png)

开始    docker会在本机寻找镜像      判断有没有镜像  

![image-20200722102838466](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722102838466.png)

### 底层原理

docker是怎么工作的？

docker是一个client -server结构的系统 docker的守护进程运行在主机上，通过socket从客户端访问！

dockerServer接收到 dockerClient的命令，就会执行这个命令！

![image-20200722103947652](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722103947652.png)

Docker为什么比vm快

1、docker有着比虚拟机更少的抽象层

2、docker利用的是宿主机的内核，vm需要是Guest OS

![image-20200722104639789](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722104639789.png)

所以说，新建一个容器的时候，docker不需要想虚拟机一样重新加载一个操作系统内核，避免引导，虚拟机是加载GuestOS，分钟级别的，而docker是利用宿主的操作系统吗，省略了这个复杂的过程，妙级！

![image-20200722105954079](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200722105954079.png)

## docker的常用命令

### 帮助命令

```
docker version     #显示版本信息

docker info   	   #显示docker系统信息

docker 命令 --hepl  #万能命令

```

帮助文档地址：https://docs.docker.com/reference/

### 镜像命令

##### docker image 查看本地镜像

```
[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        6 months ago        13.3kB

#解释
REPOSITORY  镜像的仓库源
TAG  		镜像标签
IMAGE ID	镜像ID
CREATED		镜像创建时间
SIZE		镜像的大小

#可选项
[root@localhost ~]# docker images --help

Usage:	docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             #列出所以镜像
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           #只显示镜像的ID
  
  
```

##### docker search 搜索镜像

```
[root@localhost ~]# docker search mysql
NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   9755                [OK]                
mariadb                           MariaDB is a community-developed fork of MyS…   3562                [OK]      

#可选项 通过搜索来过滤
--filter=SIZE=3000    搜索出来的镜像就是SIZE大于3000
[root@localhost ~]# docker search mysql --filter=SIZE=3000
Error response from daemon: Invalid filter 'size'
[root@localhost ~]# docker search mysql --filter=STARS=3000
NAME                DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql               MySQL is a widely used, open-source relation…   9755                [OK]                
mariadb             MariaDB is a community-developed fork of MyS…   3562                [OK]                
[root@localhost ~]# docker search mysql --filter=STARS=5300
NAME                DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql               MySQL is a widely used, open-source relation…   9755                [OK]  
```

#####  docker pull 下载

```
[root@localhost ~]# docker pull --help

Usage:	docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Pull an image or a repository from a registry

Options:
  -a, --all-tags                Download all tagged images in the repository
      --disable-content-trust   Skip image verification (default true)
      --platform string         Set platform if server is multi-platform capable
  -q, --quiet                   Suppress verbose output
  
  下载镜像   docker pull 镜像名(:tag)
[root@localhost ~]# docker pull mysql
Using default tag: latest             #如果不写tag 默认latest
latest: Pulling from library/mysql	  
8559a31e96f4: Pull complete 		  #分层下载：docker iamage的核心 联合文件系统
d51ce1c2e575: Pull complete 
c2344adc4858: Pull complete 
fcf3ceff18fc: Pull complete 
16da0c38dc5b: Pull complete 
b905d1797e97: Pull complete 
4b50d1c6b05c: Pull complete 
571e8a282156: Pull complete 
e7cc823c6090: Pull complete 
89f6364a8689: Pull complete 
55e5b10f33a4: Pull complete 
68129e7a0316: Pull complete 
Digest: sha256:c455bbcaa8b9c5c636c45f6184f970caeb3d8b545a0390e1b72a253e07aef8fd		#签名
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest    #真实地址

# 等价于它
docker pull mysql 
docker pull docker.io/library/mysql:latest

# 指定版本下载
docker pull mysql:5.7

[root@localhost ~]# docker pull mysql:5.7
5.7: Pulling from library/mysql
8559a31e96f4: Already exists 
d51ce1c2e575: Already exists 
c2344adc4858: Already exists 
fcf3ceff18fc: Already exists 
16da0c38dc5b: Already exists 
b905d1797e97: Already exists 
4b50d1c6b05c: Already exists 
0a52a5c57cd9: Pull complete 
3b816a39d367: Pull complete 
13ee22d6b3bb: Pull complete 
e517c3d2ba35: Pull complete 
Digest: sha256:ea560da3b6f2f3ad79fd76652cb9031407c5112246a6fb5724ea895e95d74032
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7

```

##### docker rmi 删除镜像

```
选择ID删除镜像 删除指定容器  空格加id删除
[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mysql               latest              5ac22cccc3ae        31 hours ago        544MB
mysql               5.7                 d05c76dbbfcf        8 days ago          448MB
hello-world         latest              bf756fb1ae65        6 months ago        13.3kB
[root@localhost ~]# docker rmi -f  d05c76dbbfcf
Untagged: mysql:5.7
Untagged: mysql@sha256:ea560da3b6f2f3ad79fd76652cb9031407c5112246a6fb5724ea895e95d74032
Deleted: sha256:d05c76dbbfcf3e1d969eecc04d0aa461e0f95204f6833f62edb73cca7b62fcd4
Deleted: sha256:840de3dd46e7b6203f85075d3bbc784b151e0de21f77dfa37744fc8edeaf766b
Deleted: sha256:7438475d185887f36358065f793c5699b459bc13271aee0b606b9d68230452ef
Deleted: sha256:323859cca1e70d6db23f15dd1d6c0c66e08f116147477663f3be2d94c89ba3a8
Deleted: sha256:14a1c67348bc38b8f7316be7993dea0c03c5375e7728dcffb2da90ceed74c1f0

递归删除  容器ID  
[root@localhost ~]# docker rmi -f $(docker images -aq)
Untagged: mysql:latest
Untagged: mysql@sha256:c455bbcaa8b9c5c636c45f6184f970caeb3d8b545a0390e1b72a253e07aef8fd
Deleted: sha256:5ac22cccc3ae67ca42ed92b55c8fa7c68967ec6b875d15d761467d40097368b6
Deleted: sha256:86c56823286628a66aa344188924e576c85b94b4734c418a6a0e123068170c4f
Deleted: sha256:28f36292125ccc90319e3153c5eb83d374d2875c9e46a7538568fc32458ec034
Deleted: sha256:291205778291931aee087875f7d1c30382db776809095e30260079f998025426
Deleted: sha256:620e22d166022716e2d8984417abecdd637b30e3815e9f3b543e93cdde1d09e9
Deleted: sha256:f67b13ad42222e45e0eaf18adbc9f408e2dc32cdb814be4f3243a6ab0b5bcd0a
Deleted: sha256:09687cd9cdf4c704fde969fdba370c2d848bc614689712bef1a31d0d581f2007
Deleted: sha256:b704a4a65bf536f82e5d8b86e633d19185e26313de8380162e778feb2852011a
Deleted: sha256:c37206160543786228aa0cce738e85343173851faa44bb4dc07dc9b7dc4ff1c1
Deleted: sha256:12912c9ec523f648130e663d9d4f0a47c1841a0064d4152bcf7b2a97f96326eb
Deleted: sha256:57d29ad88aa49f0f439592755722e70710501b366e2be6125c95accc43464844
Deleted: sha256:b17c024283d0302615c6f0c825137da9db607d49a83d2215a79733afbbaeb7c3
Deleted: sha256:13cb14c2acd34e45446a50af25cb05095a17624678dbafbcc9e26086547c1d74
Untagged: hello-world:latest
Untagged: hello-world@sha256:49a1c8800c94df04e9658809b006fd8a686cab8028d33cfba2cc049724254202
Deleted: sha256:bf756fb1ae65adf866bd8c456593cd24beb6a0a061dedf42b26a993176745f6b


```



### 容器命令

###### 说明 我们有了镜像才可以创建容器，linux，下载一个centos镜像来测试学习

```
docker pull centos

```

###### 新建容器并启动

```
docker run (可选参数) image

#参数说明
-- name="name"  容器名字 tamcat01 tamcat02 用来区分容器
-d      		后台方式运行
-it				使用交互方式运行，进入容器查看内容
-P				指定容器的端口 -p 8080:8080
		-p  主机端口：容器端口（常用）
		-p	ip端口：容器端口
		-p  容器端口
		容器端口


-p				随机指定端口


#测试  启动并进入容器
[root@localhost ~]# docker run -it centos /bin/bash
[root@d3a648324a43 /]# 
[root@d3a648324a43 /]# ls  #查看容器内的centos  基础版本很多命令不是完善的
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr


#从容器退出主机
[root@d3a648324a43 /]# exit从容器退出主机
exit
[root@localhost /]# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr

```

###### 列出列表中所以运行的容器

###### docker ps 命令

```
# docker ps 命令
   #列出当前正在运行的容器
-a #列出当前正在运行的容器+带出历史运行过的容器
-n=? # 显示最近创建容器
-q #只显示容器的编号



[root@localhost /]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@localhost /]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS               NAMES
d3a648324a43        centos              "/bin/bash"         8 minutes ago       Exited (130) 4 minutes ago                       kind_benz
899e142d1940        bf756fb1ae65        "/hello"            4 hours ago         Exited (0) 4 hours ago                           musing_wilson


```

###### 退出容器

```
exit   # 直接容器停止并退出

Ctrl+P+Q  #容器不停止退出

```

###### 删除容器

```
docker rm 容器id						#删除指定的容器，不能删除正在运行容器 rm -f

docker rm -f  $(docker ps -aq)		 #删除所有的容器

docker ps -a -q|xargs docker.rm  	 #删除所有的容器

```

###### 启动和停止容器的操作  clear 清楚页面

```
docker start 容器id       #启动容器
docker restart 容器id		#重启容器
docker stop  容器id		#停止当前正在运行容器
docker kill 容器id		#强制停止当前容器

```

### 常用其他命令

###### 后台启动命令

```
#命令 docker run -d 镜像名

[root@localhost /]# docker run -d centos

#问题docker ps 发现centos 停止了


#常见的坑 docker 容器使用后台运行，就必须要有一个前台进程，容器发现没有应用，就会自动停止
#nginx 容器启动后 发现自己没有提供服务，就会立即停止，就是没有程序了

```

###### 查看日志

```
docker logs
docker logs -f -t --tail 容器，没有日志

#自己编写一段shell脚本
[root@localhost /]# docker run -d centos /bin/sh -c "while true;do echo pengzhizhong;sleep 1;done"


#容器id 
[root@localhost /]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
59bb72491fd9        centos              "/bin/sh -c 'while t…"   2 seconds ago       Up 2 seconds                            suspicious_albattani


#显示日志
-tf		#显示所有日志
--tail number# 要显示使用日志
[root@localhost /]# docker logs -tf --tail 10  59bb72491fd9 


```

###### 查看容器中进程信息ps

top  命令

```
[root@localhost /]# docker top 59bb72491fd9
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                17021               17004               0                   15:26               ?                   00:00:00            /bin/sh -c while true;do echo pengzhizhong;sleep 1;done
root                19316               17021               0                   16:00               ?                   00:00:00            /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1



```

###### 查看镜像源数据

docker inspect  容器Id

```
#命令
docker inspect  容器Id

#测试
root@localhost /]# docker inspect 59bb72491fd9 
[
    {
        "Id": "59bb72491fd936accca27ccafd1e218bfa70ffbe66cba4352667927f6bd2b573",
        "Created": "2020-07-22T07:26:15.358870836Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true;do echo pengzhizhong;sleep 1;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 17021,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-07-22T07:26:15.729505543Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:831691599b88ad6cc2a4abbd0e89661a121aff14cfa289ad840fd3946f274f1f",
        "ResolvConfPath": "/var/lib/docker/containers/59bb72491fd936accca27ccafd1e218bfa70ffbe66cba4352667927f6bd2b573/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/59bb72491fd936accca27ccafd1e218bfa70ffbe66cba4352667927f6bd2b573/hostname",
        "HostsPath": "/var/lib/docker/containers/59bb72491fd936accca27ccafd1e218bfa70ffbe66cba4352667927f6bd2b573/hosts",
        "LogPath": "/var/lib/docker/containers/59bb72491fd936accca27ccafd1e218bfa70ffbe66cba4352667927f6bd2b573/59bb72491fd936accca27ccafd1e218bfa70ffbe66cba4352667927f6bd2b573-json.log",
        "Name": "/suspicious_albattani",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/5e8409bdc882274f69aa7a7d8263a3a914a90a5b438133aa3f6eab4723b079bd-init/diff:/var/lib/docker/overlay2/cf3cd4182bb1fffdbe306c271986f6c70589060341abca7c8e2a4273f225b7d7/diff",
                "MergedDir": "/var/lib/docker/overlay2/5e8409bdc882274f69aa7a7d8263a3a914a90a5b438133aa3f6eab4723b079bd/merged",
                "UpperDir": "/var/lib/docker/overlay2/5e8409bdc882274f69aa7a7d8263a3a914a90a5b438133aa3f6eab4723b079bd/diff",
                "WorkDir": "/var/lib/docker/overlay2/5e8409bdc882274f69aa7a7d8263a3a914a90a5b438133aa3f6eab4723b079bd/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "59bb72491fd9",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true;do echo pengzhizhong;sleep 1;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20200611",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "8894abbf6b0ebd5f46a428c8705d493e9e95469778a817f648863edf1d2d0655",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/8894abbf6b0e",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "f4e382f8a9b460ec0b5a5813655123d84d7808ae432a6b9173c73a9b00d8088c",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "e1e1bff7630a2cc8b8b902fc8171ba7b268c49ad51de3928013d19cff9e89247",
                    "EndpointID": "f4e382f8a9b460ec0b5a5813655123d84d7808ae432a6b9173c73a9b00d8088c",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

###### 进入当前正在运行的容器

```
#我们的容器都是使用后台方式运行的，需要进入容器，修改一些 配置

#命令

docker exec -it 容器id  bashShell

#测试
[root@localhost /]# docker ps
CONTAINER ID        IMAGE               COMMAND                n  CREATED             STATUS              PORTS               NAMES
260c47e63af0        centos              "/bin/sh -c 'while t…"   5 seconds ago       Up 4 seconds                            admiring_goodall
[root@localhost /]# docker exec -it 260c47e63af0 /bin/bash
[root@260c47e63af0 /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr


#第二方式 
docker attch 容器id
#测试
[root@localhost ~]# docker attach sad58465
当前写的死循环代码

#docker exec        #进入容器后开启新的终端，可以在里面操作（常用）
#docker attach		#进入容器正在执行的终端，不会启动新的进程

```

从容器内拷贝文件到主机上

```
docker cp 容器id：容器内路径  目的主机路径


touch 创建文本


#查看当前主机目录下


[root@localhost home]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
#启动容器进入容器
[root@localhost home]# docker run -it centos /bin/bash
[root@9fc363c4e31b /]# ls
bin  etc   lib	  lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr
[root@9fc363c4e31b /]# cd home/
#在容器创建文件
[root@9fc363c4e31b home]# touch test.java
[root@9fc363c4e31b home]# ls
test.java
#退出容器
[root@9fc363c4e31b home]# exit
exit
#查看容器IP
[root@localhost home]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                           PORTS               NAMES
9fc363c4e31b        centos              "/bin/bash"              4 minutes ago    
# 将文件拷贝到主机上
[root@localhost home]# docker cp 9fc363c4e31b:/home/test.java /home
[root@localhost home]# ls
pengzhizhong.java  test.java  wanght


#拷贝是一个手动过程，使用 -V 卷的技术，可以实现

```

###### 小结

![image-20200723084954606](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723084954606.png)

```
docker version`查看docker版本
docker info`查看docker详细信息
docker --help`查看docker命令
docker images查看docker镜像

```

![image-20200723085456334](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723085456334.png)

PEPOSITORY：镜像的仓库源
TAG：镜像的标签
IMAGE ID：镜像ID
CREATED：镜像创建时间
SIZE：镜像大小

```
docker images -a`列出本地所有的镜像
`docker images -p`只显示镜像ID
`docker images --digests`显示镜像的摘要信息
`docker images --no-trunc`显示完整的镜像信息

```

![image-20200723085616257](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723085616257.png)

`docker search tomcat`从Docker Hub上查找tomcat镜像

![image-20200723085642012](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723085642012.png)

```
docker search -s 30 tomcat从Docker Hub上查找关注度大于30的tomcat镜像
docker pull tomcat从Docker Hub上下载tomcat镜像。等价于：docker pull tomcat:latest
docker commit -m "提交的描述信息" -a "作者" 容器ID 要创建的目标镜像名称:[标签名]提交容器使之成为一个新的镜像。
如：docker commit -m "新的tomcat" -a "lizq" f9e29e8455a5 mytomcat:1.2
docker rmi hello-world从Docker中删除hello-world镜像
docker rmi -f hello-world从Docker中强制删除hello-world镜像
docker rmi -f hello-world nginx从Docker中强制删除hello-world镜像和nginx镜像
docker rmi -f $(docker images -p)通过docker images -p查询到的镜像ID来删除所有镜像
三、容器命令。
docker run [OPTIONS] IMAGE根据镜像新建并启动容器。IMAGE是镜像ID或镜像名称
OPTIONS说明：
 --name=“容器新名字”：为容器指定一个名称
 -d：后台运行容器，并返回容器ID，也即启动守护式容器
 -i：以交互模式运行容器，通常与-t同时使用
 -t：为容器重新分配一个伪输入终端，通常与-i同时使用
 -P：随机端口映射
 -p：指定端口映射，有以下四种格式：
  ip:hostPort:containerPort
  ip::containerPort
  hostPort:containerPort
  containerPort
docker ps列出当前所有正在运行的容器
docker ps -a列出所有的容器
docker ps -l列出最近创建的容器
docker ps -n 3列出最近创建的3个容器
docker ps -q只显示容器ID
docker ps --no-trunc显示当前所有正在运行的容器完整信息
exit退出并停止容器
Ctrl+p+q只退出容器，不停止容器
docker start 容器ID或容器名称启动容器
docker restart 容器ID或容器名称重新启动容器
docker stop容器ID或容器名称停止容器
docker kill 容器ID或容器名称强制停止容器
docker rm 容器ID或容器名称删除容器
docker rm -f 容器ID或容器名称强制删除容器
docker rm -f $(docker ps -a -q)删除多个容器
docker logs -f -t --since --tail 容器ID或容器名称查看容器日志
如：docker logs -f -t --since=”2018-09-10” --tail=10 f9e29e8455a5
 -f : 查看实时日志
 -t : 查看日志产生的日期
 --since : 此参数指定了输出日志开始日期，即只输出指定日期之后的日志
 --tail=10 : 查看最后的10条日志
docker top 容器ID或容器名称查看容器内运行的进程
docker inspect 容器ID或容器名称查看容器内部细节
docker attach 容器ID进到容器内
docker exec 容器ID进到容器内
docker cp 容器ID:容器内的文件路径 宿主机路径从容器内拷贝文件到宿主机.
如：docker cp f9e29e8455a5:/tmp/yum.log /root

```

###### 练习

###### docker 安装nginx

搜索nginx

```
[root@localhost ~]# docker search nginx
NAME                               DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                              Official build of Nginx.                        13502               [OK]   

```

安装nginx

```
[root@localhost ~]# docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
6ec8c9369e08: Pull complete 
d3cb09a117e5: Pull complete 
7ef2f1459687: Pull complete 
e4d1bf8c9482: Pull complete 
795301d236d7: Pull complete 
Digest: sha256:0e188877aa60537d1a1c6484b8c3929cfe09988145327ee47e8e91ddf6f76f5c
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

```

查看nginx

```
docker images

```

启动nginx    

```
[root@localhost ~]# docker run -d --name nginx01 -p 3344:80 nginx
b2b45a0979be454a25845452b7f364f7047282600ca06ffcc75254d1ecb60947

```

运行测试

```
[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              8cf1bfb43ff5        22 hours ago        132MB
centos              latest              831691599b88        5 weeks ago         215MB
^C[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
# -d 是后台运行
#--name 给容器起名字
#-p 客主机端口，容器内部端口
[root@localhost ~]# docker run -d --name nginx01 -p 3344:80
"docker run" requires at least 1 argument.
See 'docker run --help'.

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container
[root@localhost ~]# docker run -d --name nginx01 -p 3344:80 nginx
b2b45a0979be454a25845452b7f364f7047282600ca06ffcc75254d1ecb60947
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
b2b45a0979be        nginx               "/docker-entrypoint.…"   2 minutes ago       Up 2 minutes        0.0.0.0:3344->80/tcp   nginx01
[root@localhost ~]# curl localhost:3344

```

![image-20200723092608887](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723092608887.png)

进入nginx

```
root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
b2b45a0979be        nginx               "/docker-entrypoint.…"   14 minutes ago      Up 14 minutes       0.0.0.0:3344->80/tcp   nginx01
[root@localhost ~]# docker exec -it nginx01 /bin/bash
root@b2b45a0979be:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@b2b45a0979be:/# cd etc/nginx
root@b2b45a0979be:/etc/nginx# ls
conf.d		koi-utf  mime.types  nginx.conf   uwsgi_params
fastcgi_params	koi-win  modules     scgi_params  win-utf

```

退出nginx

```
root@b2b45a0979be:/etc/nginx# exit
exit
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
b2b45a0979be        nginx               "/docker-entrypoint.…"   20 minutes ago      Up 20 minutes       0.0.0.0:3344->80/tcp   nginx01

```

停止nginx

```
[root@localhost ~]# docker stop b2b45a0979be
b2b45a0979be
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

```

改配置文件十分麻烦，我要是可以在容器外部提供一个映射路径，达到在容器修改文件名，容器内部就可以自动修改？-v 数据卷

###### docker 来装一个tomcat

查看tomcat

```
docker search tomcat

```

下载tomcat

```
下载1
docker pull tomcat

#官方的使用
$ docker run -it --rm tomcat:9.0

#我们之前的启动都是后台，停止了容器之后，容器还是可以查到  docker run -it --rm,一般用来测试用完就删除

#下载在启动
$docker pull tomcat

[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              8cf1bfb43ff5        23 hours ago        132MB
tomcat              9.0                 df72227b40e1        6 days ago          647MB
tomcat              latest              df72227b40e1        6 days ago          647MB
centos              latest              831691599b88        5 weeks ago         215MB

$启动运行
docker run -d -p 3355:8080 --name tomcat01 tomcat

#测试访问外网没有问题
#进入tomcat
[root@localhost ~]# docker exec -it tomcat01 /bin/bash
root@b459fdbf6eab:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work

#发现问题 linux命令少了2、没有webapps  阿里云镜像原因，默认是最小的镜像，所有把没有必要的删除了
#保证最小可运行环境

因为webapps没有文件所有网站是404
root@b459fdbf6eab:/usr/local/tomcat# cd webapps
root@b459fdbf6eab:/usr/local/tomcat/webapps# ls
root@b459fdbf6eab:/usr/local/tomcat/webapps# cd  ..
root@b459fdbf6eab:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@b459fdbf6eab:/usr/local/tomcat# cd webapps.dist/
root@b459fdbf6eab:/usr/local/tomcat/webapps.dist# ls
ROOT  docs  examples  host-manager  manager
root@b459fdbf6eab:/usr/local/tomcat/webapps.dist# cd ..
root@b459fdbf6eab:/usr/local/tomcat# cp -r webapps.dist/* webapps        
root@b459fdbf6eab:/usr/local/tomcat# cd webapps
root@b459fdbf6eab:/usr/local/tomcat/webapps# ls
ROOT  docs  examples  host-manager  manager

```

思考问题我们以后要部署项目，如果每次都要进入容器是不是十分麻烦 我要是可以在容器外部提供一个映射路径webapps，我们在外部放置项目 ，就自动同步内部就好了

###### 部署es +kibana

#es 暴露端口很多

#es 十分耗内存

#es的数据一般需要放置安全目录 ！挂载   --net somenetwork网络设置

```
下载启动elasticsearch
$ docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2

#启动就 linux就卡 docker stats查看cpu的状态


#es 是十分耗内存 启动1.几g

#停止整个docker

查看 cpu
$docker stats
CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
b38d93ece688        elasticsearch       0.21%               1.238GiB / 1.929GiB   64.17%              648B / 0B           0B / 0B             44
^C
#测试一下es链接成功
[root@localhost ~]# curl localhost:9200
{
  "name" : "b38d93ece688",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "RhoH8yDSQgyedHW6ctACkA",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

#赶紧关闭，增加内存的限制


```

使用docker 连接Es

![image-20200723141728462](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723141728462.png)

#赶紧关闭，增加内存的限制

![image-20200723145801720](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723145801720.png)



#赶紧关闭，增加内存的限制  修改配置文件 -e 环境配置修改

```
#赶紧关闭，增加内存的限制  修改配置文件 -e 环境配置修改
[root@localhost ~]# docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node"  -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
b96244c27619304b1d6be7562db07f2175f2c49f2b09b550fbbb3e4e1bd7e0d0

#查看docker ES
docker stats 
[root@localhost ~]# docker stats b96244c27619
CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
b96244c27619        elasticsearch02     1.90%               389.3MiB / 1.929GiB   19.70%              648B / 0B           0B / 0B             45

```

```
[root@localhost ~]# curl localhost:9200
{
  "name" : "b96244c27619",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "wKAMcHljSqilOdwCH8UAow",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

```

###### 可视化

portainer(先用这个)

Rancher(CI?CD再用)

什么portainer？

docker图形化的界面管理工具！提供一个后台面板供我们操作

```
# docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer 

```

访问测试：外网：8088 http://192.168.40.128:8088/#/init/admin

通过他访问

注册账号：

密码

![image-20200723153533391](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723153533391.png)

登入进去了 选择本地

![image-20200723153847536](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723153847536.png)

进去面板

![image-20200723153932973](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723153932973.png)



## Docker镜像讲解

镜像（Mirroring）是一种文件存储形式，是冗余的一种类型，一个[磁盘](https://baike.baidu.com/item/磁盘/2842227)上的数据在另一个磁盘上存在一个完全相同的副本即为镜像。可以把许多文件做成一个镜像文件，与GHOST等程序放在一个盘里用[GHOST](https://baike.baidu.com/item/GHOST/20443952)等软件打开后，又恢复成许多文件，RAID 1和RAID 10使用的就是镜像。常见的镜像[文件格式](https://baike.baidu.com/item/文件格式)有ISO、BIN、IMG、TAO、DAO、CIF、FCD。

查看镜像信息

[root@localhost ~]# docker image inspect redis:latest



## Commit镜像

```
docker commit  提交容器成为一个新的副本

#命令和git原理类似
docker commit -m="提交的描述信息"  -a="作者" 容器id 目标镜像名，[TAC]

```

实战测试

1、启动默认的tomcat

```
[root@localhost ~]# docker run -it -p 8080:8080 tomcat
退出tomcat

exit

进入tomcat

[root@localhost ~]# docker exec -it 7cfc11ac6cb2 /bin/bash
root@7cfc11ac6cb2:/usr/local/tomcat# cd webapps

2、发现这个默认的tomcat 是没有webapps应用，镜像的原因，官方的镜像默认webapps下面是没有文件的
root@7cfc11ac6cb2:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@7cfc11ac6cb2:/usr/local/tomcat# cd webapps
root@7cfc11ac6cb2:/usr/local/tomcat/webapps# ls

3、我自己拷贝进行了基本的文件
root@7cfc11ac6cb2:/usr/local/tomcat/webapps# cd ..
root@7cfc11ac6cb2:/usr/local/tomcat# cp -r webapps.dist/* webapps
root@7cfc11ac6cb2:/usr/local/tomcat# cd webapps
root@7cfc11ac6cb2:/usr/local/tomcat/webapps# ls
ROOT  docs  examples  host-manager  manager


4、将我们操作过程的容器通过tomcat提交为一个镜像 ！我们以后 就使用我们修改过的镜像即可，这个是我们自己的一个修改的镜像
[root@localhost ~]# docker commit -a="add webapps app" 7cfc11ac6cb2 tomcat02:1.0
sha256:bd03df5abbe3e9757052afbfe6bbd1180bb355a2b3893e4e931e0b4400e9701a
[root@localhost ~]# docker images
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
tomcat02              1.0                 bd03df5abbe3        24 seconds ago      652MB
tomcat                9.0                 df72227b40e1        6 days ago          647MB
tomcat                latest              df72227b40e1        6 days ago          647MB

```

如果你想要保存当前容器的状态，就可以通过commit来提交，获取一个镜像就好比我们以前学习vm时候快照

## 容器数据卷

#### 什么是容器卷

将应用和环境打包一个镜像！

数据？如果数据在容器中，那么我们容器删除，数据就会丢失！==需求：数据可以持久化==

msql容器删了，删库跑路！需求mysql数据可以存储在本地

容器之间可以有一个数据共享的技术！docker容器中产生的数据，同步到本地！

这技术卷技术！目录的挂载，将我们容内的目录，挂载到linux上面！

![image-20200723173130629](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200723173130629.png)

总结一句话 容器的持久化和同步操作！容器间也是可以数据共享！

### 使用数据卷

方式一：直接使用命令来挂载 -v

docker run -it -v 主机目录 容器内端口

```
测试
[root@localhost home]# docker run -it -v /home/ceshi:/home centos /bin/bash



查看挂载卷 命令
[root@localhost home]# docker inspect 6970aebb1bd5

#启动起来时候我们可以通过docker inspect 容器id

```

![image-20200724092437127](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724092437127.png)

测试文件双向绑定 数据卷的技术

![image-20200724092939364](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724092939364.png)

再来测试

```
启动centos容器 
[root@localhost home]# docker start 6970aebb1bd5
6970aebb1bd5
进入容器 
[root@localhost home]# docker attach 6970aebb1bd5
[root@6970aebb1bd5 /]# 



查看
[root@localhost ceshi]# ls
test.java
编辑java文件
[root@localhost ceshi]# vim test.java 
看文件类写什么东西
[root@6970aebb1bd5 home]# cat test.java 
hello linux docker 

```

关闭镜像 在镜像共层里修改文件有可以修改文件

1、停止容器

2、宿主机上修改文件

3、启动容器

4、容器内的数据依据旧的同步

![image-20200724135041487](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724135041487.png)

好处我们以后修改只需要在本地修改即可，容器内会自动同步

#### 实战mysql 

思考：mysql的数据持久化的问题

```
获取镜像
[root@localhost ~]# docker pull mysql.5:7


官方的测试mysql $ docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag    -e是配置



-d 是后台运行  
-p是端口映射 
-v数据卷 
-e 环境配置
--name名字
运行容器需要数据挂载 安装MySQL需要配置密码的
[root@localhost ~]# docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
ae0a9515b4bc17fbe1907c5557af1df6d2ab3b21a42ef17eb01337b21fd3df32


启动成功之后，我们在本地使用navicat15 来链接测试
navicat15连接到服务器的3310---和容器的3306映射，这个我们可以使用了


```

![image-20200724154651998](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724154651998.png)

![image-20200724154730803](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724154730803.png)

##### 具名挂载和匿名挂载

匿名挂载

-v 容器内路径

```
启动nginx 
docker run -d -P --name nginx01 -v /ect/nginx nginx

查看nginx状态
docker volume --hele

查看所有卷的情况
docker volume ls
root@localhost /]# docker volume ls
DRIVER              VOLUME NAME
local               6d5a399cbe6b9d9ce22969e39f04266c2c31f5659b751c2104304d026ebebb91

```

匿名挂载

```
匿名挂载命令
[root@localhost /]# docker run -d -P --name nginx01 -v /ect/nginx nginx
Digest: sha256:0e188877aa60537d1a1c6484b8c3929cfe09988145327ee47e8e91ddf6f76f5c
c9c8ab21bdab8aea4c312ef873cb6035577e7c2310dcb216176cf9f8ba395884

```

![image-20200724162409930](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724162409930.png)

这里发现，这种就是里面挂载，我们在-v 只写了容器内的路径，没有写容器外的路径

具名命令

```
[root@localhost /]# docker run -d -P --name nginx02 -v pzz:/etc/nginx nginx
588203564c007f36eb1c38fe28c17b7657dcb6bc1272f64e9b00a10a0c6d89a1

```

![image-20200724162252865](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724162252865.png)

通过 -v 卷名：容器内路径

查看一下卷

命令 

docker volume inspect pzz

![image-20200724163139858](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200724163139858.png)

所有docker容器的卷，没有指定目录的情况下都在/ver/lib/docker/volumes

[root@localhost /]# cd /var/lib/docker/

查看所有文件

```
[root@localhost docker]# ls
builder   containers  network   plugins   swarm  trust
buildkit  image       overlay2  runtimes  tmp    volumes
[root@localhost docker]# cd volumes/
[root@localhost volumes]# ls
6d5a399cbe6b9d9ce22969e39f04266c2c31f5659b751c2104304d026ebebb91
9c9f85762dc014e2c2b06604d3075df6ff4e3a43bc36868c88784f100421e828
ac6bde82eea6a2cb25ab5c49a7518079ee08c9fe29abcb63e029be2d2aca695a
d0994a0a7f1d20e796f86ca8bc88df1f6f541e0d6ab1877f1d586619abbf81e2
metadata.db
pzz
[root@localhost volumes]# cd pzz
[root@localhost pzz]# ls
_data
[root@localhost pzz]# cd _data/

```

查看nginx文件

```
[root@localhost _data]# ls
conf.d          koi-utf  mime.types  nginx.conf   uwsgi_params
fastcgi_params  koi-win  modules     scgi_params  win-utf

```

查看nginx配置文件

```
root@localhost _data]# cat nginx.conf 

user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

```

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    
    access_log  /var/log/nginx/access.log  main;
    
    sendfile        on;
    #tcp_nopush     on;
    
    keepalive_timeout  65;
    
    #gzip  on;
    
    include /etc/nginx/conf.d/*.conf;
    

扩展：

```
通过 -v 容器内的路径，ro rw 改变读写权限 
ro readonly 只读
rw readwrite 可读可写

一旦这个了设置了设置容器权限 容器对我们挂载出来的内容就有限定
docker run -d -P --name02 -v pzz:/etc/nginx:ro nginx
docker run -d -P --name02 -v pzz:/etc/nginx:rw nginx

ro 只要看到ro就说明这个路径只能宿主机来操作，容器内部是无法操作

```

## 初识dockerfile

dockerfile就是用来构建docker镜像的文件|命令脚本先体验一下

```
创建文件
$ mkdir docker-test-volume
查看路径
[root@localhost docker-test-volume]# pwd
/home/docker-test-volume
编辑dockerfile1 文档
[root@localhost docker-test-volume]# vim dockerfile1 

```

通过脚本可以生成镜像，镜像是一层一层的，脚本一个个的命令，每个命令都是一层！

创建一个dockerfile文件 ，名字可以随机 建议dockerfile

文件中的内容  指令建议（大写）参数

```
脚本命令都是大写
FROM centos

VOLUME ["volume01","volume02"]

CMD echo "---end---"

CMD /bin/bash

这里的每个命令，就是镜像的一层

```

执行脚本命令

```
$ docker build -f /home/docker-test-volume/dockerfile1 -t pzz/centos:1.0 .

```

命令执行成功

![image-20200728102305469](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728102305469.png)

启动自己的容器

```
[root@localhost docker-test-volume]# docker run -it bac7455cf94f /bin/bash
[root@a7eb83e6293a /]# 

```

![image-20200728103226110](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728103226110.png)

这个卷和外部一定有一个同步的目录

![image-20200728103356831](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728103356831.png)

在容器内部创建文件

```
root@localhost docker-test-volume]# clear
[root@localhost docker-test-volume]# docker run -it bac7455cf94f /bin/bash
[root@26778eab87cb /]# cd v
var/      volume01/ volume02/ 
[root@26778eab87cb /]# cd volume01
[root@26778eab87cb volume01]# touch container.txt
[root@26778eab87cb volume01]# ls
container.txt
[root@26778eab87cb volume01]# 

```

在容器外部查看容器运行

```
[root@localhost /]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
26778eab87cb        bac7455cf94f        "/bin/bash"         3 minutes ago       Up 3 minutes                            focused_pare

查看在运行容器的信息
[root@localhost /]# docker inspect 26778eab87cb 


```

查看卷的挂载路径

![image-20200728104144669](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728104144669.png)

测试一下刚才的文件是否同步出去了

这种方式我们未来使用非常的多，因为我们通常会构建自己的镜像

假设构建镜像时候没有挂卷，要手动镜像挂载-v卷名：内容内路径

```
[root@localhost /]# cd /var/lib/docker/volumes/c041241693fec76c7fc4e1099126a8f4b31b4552676611a5ff43d10fac3569e4/_data
[root@localhost _data]# ls
container.txt
[root@localhost _data]# 

```

## 数据卷的容器

多个MySQL同步数据

![image-20200728105453116](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728105453116.png)

启动3个容器，通过我们刚才自己写的镜像启动

启动docker01 

启动命令

docker run -it --name docker01 pzz/centos:1.0

![image-20200728110136973](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728110136973.png)

启动docker02

启动命令

```
[root@localhost /]# docker run -it --name docker02 --volumes-from docker01 pzz/centos:1.0

```

![image-20200728110854810](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728110854810.png)

dockers01容器创建在volume01中docker01文件

![image-20200728111315984](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728111315984.png)

docker02查看docker01

![image-20200728111436203](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728111436203.png)

创建docker03容器 容器之间都是数据继承的

![image-20200728111939782](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728111939782.png)

测试，可以删掉docker01 ，查看一下docker02和docker03是否可以访问文件

测试结果依然可以访问

数据共享是拷贝的概念



#### 测试多个mysql

多个mysql实现数据共享

```
$ docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7

```

```
$ docker run -d -p 3310:3306 -e MYSQL_ROOT_PASSWORD=123456 --name mysql02 --volumes-from mysql01 mysql:5.7

```

这个时候，可以实现两个容器数据同步

结论：

容器之间配置信息的传递，数据卷容器的生命周期一直持续到没有容器使用为止。

都是一旦你持久化到了本地 -v 这个时候，本地数据是不会删除的！

## dockerFile

### dockerFile介绍

dockerfile是用来构建docker镜像文件！命令参数脚本

构建步骤

1、编写一个docker 文件

2、docker build 构建成为一个镜像

3、docker run运行镜像

4、docker push 发布镜像（DockerHub 、阿里云镜像仓库！）

查看官方怎么做的

![image-20200728114234241](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728114234241.png)

![image-20200728114259362](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728114259362.png)

![image-20200728114335669](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728114335669.png)

很多官方镜像都是基础包，很多功能没有，我们通常会自己的镜像

官方既然可以制作镜像，那我们也可以

### DockerFile构建过程

基础知识：

1、每个保留关键字（指令）都是必须大写字母

2、执行从上到 下顺序执行

3、#表示注解

4、每个指令会创建提交一个新的镜像层，并提交！

![image-20200728133631838](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728133631838.png)

dockerflie是面向开发的，我们以后要发布项目，做镜像，就需要编写dockerflie文件，这个文件十分简单！

Docker镜像逐渐成为企业交付的标准，必须要掌握！

开发、部署、运维  缺一不可

docker：构建文件，定义了一切步骤，源代码

dcokerimages；通过dockerflie构建生成的镜像，最终发布和运行产品

docker：容器就是镜像运行起来提供服务器

### docker指令

FROM  #基础镜像，一切从这里开始构建

MAINTAINER  #镜像是谁写的，姓名+邮箱

RUM  #镜像构建的时候需要运行的命令

ADD # 步骤，tomcat镜像，这个tomcat压缩包！添加内容

WORKDIR #镜像得到工作目录

VOLUME  #挂载的目录

EXPOSE # 保留端口配置

RUN  #运行

CMD #指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代

ENTRYPOINT #指定这个容器启动的时候要运行的命令 ，可以追加命令

ONBUILD #当构建一个被继承 dockerfile这个时候就会运行 ONBUILD 的指令 触发命令

COPY #类似ADD，将我们文件拷贝到镜像中

ENV  #构建的时候设置环境变量



 ![image-20200728142216532](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728142216532.png)



实战测试

docker hub中99%镜像都是从这个基础镜像过来的FROM scratch，然后配置需要的软件和配置进行的构建

![image-20200728144704617](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728144704617.png)

创建自己的centos镜像

1、创建dockerfile文件

[root@localhost dockerfile]# vim mydockerfile-centos 
FROM centos

MAINTAINER pengzhizhong<597798954@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools


EXPOSE 80

CMD echo $MYPATH
CMD echo "---end---"
CMD /bin/bash

1.1编写dockerfile的文件

![image-20200728152106862](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728152106862.png)

2、提供这个文件构建镜像

3、执行命令

docker build  -f mydockerfile-centos -t mycentos:0.1

命令docker build -f dockerFile文件路径 -t 镜像名：[tag]

Successfully built 9571a9069424
Successfully tagged mycentos:0.1

4、测试运行一下

对比：之前的原生的centos

![image-20200728153146883](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728153146883.png)

我增加之后的镜像



![image-20200728153233873](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728153233873.png)

我们可以看到镜像构建过程

```
查看构建过程
docker history 9571a9069424

```



![image-20200728153632964](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728153632964.png)

# CMD和ENTRYPOINT区别

CMD #指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代

ENTRYPOINT #指定这个容器启动的时候要运行的命令 ，可以追加命令

测试cmd

```
#编写dockerfile文件
[root@localhost dockerfile]# vim dockerfile-cmd-test 
FROM centos
CMD {"ls","-a"}

构建镜像
[root@localhost dockerfile]# docker build -f dockerfile-cmd-test -t cmdtest .


run运行 ，发现我们的ls -a命令生效
[root@localhost dockerfile]# docker run 59a3c17c8173
.
..
.dockerenv
bin
dev
etc
home
lib
lib64
lost+found
media
mnt
opt

想追加一个命令 -l ls -al
[root@localhost dockerfile]# docker run 59a3c17c8173 -l
docker: Error response from daemon: OCI runtime create failed: container_linux.go:349: starting container process caused "exec: \"-l\": executable file not found in $PATH": unknown.
ERRO[0000] error waiting for container: context canceled 

cmd的清楚下 -l 替换了cmd{"ls","-a"}命令，-l不是命令所有报错

```

测试ENTRYPOINT

```
[root@localhost dockerfile]# vim dockerfile-cmd-entrypoint 
FROM centos
ENTRYPOINT ["ls","-a"]

```

这个是和cmd一样的

![image-20200728161643503](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728161643503.png)

我们的命令直接拼接到ENTRYPOINT命令的后面

![image-20200728161843046](C:\Users\PZZ\AppData\Roaming\Typora\typora-user-images\image-20200728161843046.png)

docker 很多命令十分相似

### 实战Tomcat镜像

1.镜像





















## docker网络



































