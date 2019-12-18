# Docker

## Docker三要素

### 镜像（Image）

　　Docker镜像（Image）就是一个**只读的模板**，镜像可以用来创建Docker容器，一个镜像可以创建很多容器。

### 容器（Container）

1. Docker利用容器（Container）独立运行一个或一组应用
2. 容器**使用镜像创建的运行实例**
3. 容器可以被启动、开始、停止、删除，每个容器之间都是相互隔离的，保证平台的安全。
4. 可以把容器看做是一个简易版的Linux环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。
5. 容器的定义和镜像几乎一摸一样，也是一堆层的统一视角，唯一区别在于容器的最上面那一层是可读可写的。

### 仓库（Repository）

1. 仓库（Repository）是集中存放镜像文件的场所。
2. 仓库（Repository）和仓库注册服务器（Registry）是有区别的，仓库注册服务器上往往存放着多个仓库，每个仓库中又包含了多个镜像，每个镜像有不同的标签（tag）。
3. 仓库分为公开仓库（Public）和私有仓库（Private）两种形式。
4. 最大的公开仓库是Docker Hub（https://hub.docker.com/），存放了数量庞大的镜像供用户下载。
5. 国内的公开仓库包括阿里云、网易云等。

## 安装

### CentOS

**Docker的安装 - 方法一**

移除旧版本：

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

![截图-1571620763](https://wimg.misiyu.cn/images/20191021/1571620764_b0f4d4347750ad5.png?x-oss-process=style/common)

添加docker **稳定版本**的 yum 软件源：

```bash
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

![截图-1571620875](https://wimg.misiyu.cn/images/20191021/1571620876_4b41c16b4496e27.png?x-oss-process=style/common)

之后更新yum源缓存，并安装 Docker

```bash
sudo yum update
sudo yum install docker-ce docker-ce-cli containerd.io
```

![截图-1571620973](https://wimg.misiyu.cn/images/20191021/1571620974_02acb489fe9e6dd.png?x-oss-process=style/common)

**之后确认docker服务正常启动**

```bash
sudo systemctl start docker
```

![截图-1571621340](https://wimg.misiyu.cn/images/20191021/1571621341_9323066831e369f.png?x-oss-process=style/common)

**可以使用此命令查看是否允许成功：**

```bash
docker info
```

![截图-1571621438](https://wimg.misiyu.cn/images/20191021/1571621439_2fcd469348b03c9.png?x-oss-process=style/common)



### Docker的启动停止

**systemctl**命令是系统服务管理器指令

启动docker：

```
systemctl start docker
```

停止docker：

```
systemctl stop docker
```

重启docker：

```
systemctl restart docker
```

查看docker状态：

```
systemctl status docker
```

开机启动：

```
systemctl enable docker
```

查看docker概要信息

```
docker info
```

查看docker帮助文档

```
docker --help
```



## 使用镜像

镜像是Docker三大核心概念中最重要的，自Docker诞生之日起镜像就是相关社区最为热门的关键词。

Docker运行容器前需要本地存在对应的镜像，如果镜像不存在，Docker会尝试先从默认镜像仓库下载（默认使用Docker Hub公共注册服务器中的仓库），用户也可以通过配置，使用自定义的镜像仓库。【如阿里云有相关的镜像服务，但需要注册配置一番】



### 获取镜像

镜像是运行容器的前提，官方的Docker Hub网站已经提供了数十万个镜像供大家开放下载。

可以使用`docker [image] pull`命令直接从Docker Hub镜像源来下载镜像。该命令的格式为

`docker [image] pull NAME[:TAG]`

如拉取一个ubuntu镜像：

```bash
docker pull ubuntu:18.04
```

![截图-1571622587](https://wimg.misiyu.cn/images/20191021/1571622588_9e510669bc2f3bf.png?x-oss-process=style/common)

> 速度慢，可参考此篇文章，建立阿里云加速器：https://www.misiyu.cn/article/122.html
>
> 或使用：
>
> ustc是老牌的linux镜像服务提供者了，还在遥远的ubuntu 5.04版本的时候就在用。ustc的docker镜像加速器速度很快。ustc docker mirror的优势之一就是不需要注册，是真正的公共服务。
>
> [https://lug.ustc.edu.cn/wiki/mirrors/help/docker](https://lug.ustc.edu.cn/wiki/mirrors/help/docker)
>
> 编辑该文件：
>
> ```
> vi /etc/docker/daemon.json  
> ```
>
> 在该文件中输入如下内容：
>
> ```json
> {
> 	"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
> }
> ```



### 查看镜像

```bash
docker images
```

![截图-1571622836](https://wimg.misiyu.cn/images/20191021/1571622837_a02a5201231866d.png?x-oss-process=style/common)

REPOSITORY：镜像名称

TAG：镜像标签

IMAGE ID：镜像ID

CREATED：镜像的创建日期（不是获取该镜像的日期）

SIZE：镜像大小

这些镜像都是存储在Docker宿主机的/var/lib/docker目录下

### 搜寻镜像

```bash
docker search [options] keyword
```

如，搜索nginx相关

```bash
docker search nginx
```

![截图-1571623260](https://wimg.misiyu.cn/images/20191021/1571623261_066bedb03bcb4e0.png?x-oss-process=style/misiyu)

NAME：仓库名称

DESCRIPTION：镜像描述

STARS：用户评价，反应一个镜像的受欢迎程度

OFFICIAL：是否官方

AUTOMATED：自动构建，表示该镜像由Docker Hub自动构建流程创建的

### 删除镜像

按镜像ID删除镜像

```bash
docker rmi 镜像ID
```

删除所有镜像

```bash
docker rmi `docker images -q`
```

## 容器相关

### 查看容器

查看正在运行的容器

```bash
docker ps
```

查看所有容器

```bash
docker ps –a
```

查看最后一次运行的容器

```bash
docker ps –l
```

查看停止的容器

```bash
docker ps -f status=exited
```



### 创建容器

创建容器常用的参数说明：

创建容器命令：docker run

 -i：表示运行容器

 -t：表示容器启动后会进入其命令行。加入这两个参数后，容器创建就能登录进去。即分配一个伪终端。

 --name :为创建的容器命名。

 -v：表示目录映射关系（**前者是宿主机目录，后者是映射到宿主机上的目录【即容器里的目录】**），可以使用多个－v做多个目录或文件映射。注意：最好做目录映射，在宿主机上做修改，然后共享到容器上。

 -d：在run后面加上-d参数,则会创建一个守护式容器在后台运行（这样创建容器后不会自动登录容器，如果只加-i -t两个参数，创建后就会自动进去容器）。

 -p：表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p做多个端口映射

（1）交互式方式创建容器

```bash
docker run -it --name=容器名称 镜像名称:标签 /bin/bash
```

这时我们通过ps命令查看，发现可以看到启动的容器，状态为启动状态  

退出当前容器

```bash
exit
```

（2）守护式方式创建容器：

```bash
docker run -di --name=容器名称 镜像名称:标签
```

登录守护式容器方式：

```bash
docker exec -it 容器名称 (或者容器ID)  /bin/bash
```



### 停止启动容器

停止容器：

```bash
docker stop 容器名称（或者容器ID）
```

启动容器：

```bash
docker start 容器名称（或者容器ID）
```



### 文件拷贝

如果我们需要将文件拷贝到容器内可以使用cp命令

```bash
docker cp 需要拷贝的文件或目录 容器名称:容器目录
```

也可以将文件从容器内拷贝出来

```bash
docker cp 容器名称:容器目录 需要拷贝的文件或目录
```



### 目录挂载

我们可以在创建容器的时候，将宿主机的目录与容器内的目录进行映射，这样我们就可以通过修改宿主机某个目录的文件从而去影响容器。
创建容器 添加-v参数 后边为   宿主机目录:容器目录，例如：

```bash
docker run -di -v /usr/local/myhtml:/usr/local/myhtml --name=mycentos3 centos:7
```

如果你共享的是多级的目录，可能会出现权限不足的提示。

这是因为CentOS7中的安全模块selinux把权限禁掉了，我们需要添加参数  --privileged=true  来解决挂载的目录没有权限的问题



### 查看容器IP地址

我们可以通过以下命令查看容器运行的各种数据

```bash
docker inspect 容器名称（容器ID） 
```

也可以直接执行下面的命令直接输出IP地址

```bash
docker inspect --format='{{.NetworkSettings.IPAddress}}' 容器名称（容器ID）
```



### 删除容器

删除指定的容器：

```bash
docker rm 容器名称（容器ID）
```



## 应用部署

### MySQL

（1）拉取mysql镜像

```bash
docker pull centos/mysql-57-centos7
```

（2）创建容器

```bash
docker run -di --name=tensquare_mysql -p 33306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
```

-p 代表端口映射，格式为  宿主机映射端口:容器运行端口

-e 代表添加环境变量  MYSQL_ROOT_PASSWORD  是root用户的登陆密码

（3）远程登录mysql

连接宿主机的IP  ,指定端口为33306 

### Tomcat

（1）拉取镜像

```bash
docker pull tomcat:7-jre7
```

（2）创建容器

创建容器  -p表示地址映射

```bash
docker run -di --name=mytomcat -p 9000:8080 
-v /usr/local/webapps:/usr/local/tomcat/webapps tomcat:7-jre7
```

### Nginx

（1）拉取镜像	

```bash
docker pull nginx
```

（2）创建Nginx容器

```bash
docker run -di --name=mynginx -p 80:80 nginx
```

### Redis

（1）拉取镜像

```bash
docker pull redis
```

（2）创建容器

```bash
docker run -di --name=myredis -p 6379:6379 redis
```