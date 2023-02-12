### Docker 简介



Docker 是一个开源的应用容器引擎，基于 Go 语言并遵从 Apache2.0 协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

Docker 从 17.03 版本之后分为 CE（Community Edition: 社区版） 和 EE（Enterprise Edition: 企业版），我们用社区版就可以了

### Docker的应用场景

+   Web 应用的自动化打包和发布。
+   自动化测试和持续集成、发布。
+   在服务型环境中部署和调整数据库或其他的后台应用。
+   从头编译或者扩展现有的 OpenShift 或 Cloud Foundry 平台来搭建自己的 PaaS 环境。

###Docker 架构

Docker 包括三个基本概念:

+   **镜像（Image）**：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
+   **容器（Container）**：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
+   **仓库（Repository）**：仓库可看成一个代码控制中心，用来保存镜像。

Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。

Docker 容器通过 Docker 镜像来创建。

| 概念                   | 说明                                       |
| -------------------- | ---------------------------------------- |
| Docker 镜像(Images)    | Docker 镜像是用于创建 Docker 容器的模板，比如 Ubuntu 系统。 |
| Docker 容器(Container) | 容器是独立运行的一个或一组应用，是镜像运行时的实体。               |
| Docker 客户端(Client)   | Docker 客户端通过命令行或者其他工具使用 Docker SDK  与 Docker 的守护进程通信。 |
| Docker 主机(Host)      | 一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。          |
| Docker Registry      | Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。Docker Hub) 提供了庞大的镜像集合供使用。一个 Docker Registry 中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本。我们可以通过 **<仓库名>:<标签>** 的格式来指定具体是这个软件哪个版本的镜像。如果不给出标签，将以 **latest** 作为默认标签。 |

### docker的基础命令

#### docker的守护进程查看

systemctl status docker

#### docker 镜像查看

docker image ls

#### docker 容器查看

docker ps

#### Docker Registry配置和查看

cat /etc/docker/daemon.json

```auto
配置私有仓库

cat>/etc/docker/daemon.json<<EOF

{

  "registry-mirrors":["http://10.24.2.30:5000","https://tnxkcso1.mirrors.aliyuncs.com"],

  "insecure-registries":["10.24.2.30:5000"]

}

EOF

```

### 在线安装docker

### 离线安装docker

一、基础环境  
1、操作系统：CentOS 7.3  
2、Docker版本：[19.03.9 官方下载地址](https://download.docker.com/linux/static/stable/x86_64/)  
3、官方参考文档：[https://docs.docker.com/install/linux/docker-ce/binaries/#install-static-binaries](https://blog.csdn.net/lcgskycby/article/details/108476333#install-static-binaries)

**二、Docker安装**

1、下载

wget https://download.docker.com/linux/static/stable/x86\_64/docker-19.03.9.tgz

注意：如果事先下载好了可以忽略这一步

2、解压

把压缩文件存在指定目录下(如root)，并进行解压

tar -zxvf docker-19.03.9.tgz

```auto
cd root
[root@localhost ~]# tar -zxvf docker-19.03.6.tgz
docker/
docker/containerd
docker/docker
docker/ctr
docker/dockerd
docker/runc
docker/docker-proxy
docker/docker-init
docker/containerd-shim

```

3、将解压出来的docker文件内容移动到 /usr/bin/ 目录下

cp docker/\* /usr/bin/

4、将docker注册为service

> cat /etc/systemd/system/docker.service

> vi /etc/systemd/system/docker.service

```auto
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target firewalld.service
Wants=network-online.target

[Service]
Type=notify
# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID

# Having non-zero Limit*s causes performance problems due to accounting overhead

# in the kernel. We recommend using cgroups to do container-local accounting.

LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity

# Uncomment TasksMax if your systemd version supports it.
# Only systemd 226 and above support this version.
#TasksMax=infinity
TimeoutStartSec=0

# set delegate yes so that systemd does not reset the cgroups of docker containers

Delegate=yes

# kill only the docker process, not all processes in the cgroup

KillMode=process

# restart the docker process if it exits prematurely

Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s


[Install]
WantedBy=multi-user.target
```

5、启动

chmod +x /etc/systemd/system/docker.service #添加文件权限并启动docker

systemctl daemon-reload #重载unit配置文件

systemctl start docker #启动Docker

systemctl enable docker.service #设置开机自启

```auto
[root@localhost ~]# vi /etc/systemd/system/docker.service
[root@localhost ~]# chmod +x /etc/systemd/system/docker.service
[root@localhost ~]# systemctl daemon-reload
[root@localhost ~]# systemctl start docker
[root@localhost ~]# systemctl enable docker.service
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /etc/systemd/system/docker.service.

```

6、验证

systemctl status docker #查看Docker状态

docker -v #查看Docker版本

docker info

```auto
[root@localhost ~]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/etc/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2021-10-09 15:25:44 CST; 29s ago
     Docs: https://docs.docker.com
 Main PID: 1916 (dockerd)
   CGroup: /system.slice/docker.service
           ├─1916 /usr/bin/dockerd
           └─1927 containerd --config /var/run/docker/containerd/containerd.toml --log-level info

Oct 09 15:25:43 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:43.671407996+08:00" level=info msg="scheme \"unix\" not r...e=grpc
Oct 09 15:25:43 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:43.671440368+08:00" level=info msg="ccResolverWrapper: se...e=grpc
Oct 09 15:25:43 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:43.671462935+08:00" level=info msg="ClientConn switching ...e=grpc
Oct 09 15:25:43 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:43.750687781+08:00" level=info msg="Loading containers: start."
Oct 09 15:25:44 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:44.072960862+08:00" level=info msg="Default bridge (docke...dress"
Oct 09 15:25:44 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:44.153444071+08:00" level=info msg="Loading containers: done."
Oct 09 15:25:44 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:44.175249299+08:00" level=info msg="Docker daemon" commit...9.03.6
Oct 09 15:25:44 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:44.175337834+08:00" level=info msg="Daemon has completed ...ation"
Oct 09 15:25:44 localhost.localdomain systemd[1]: Started Docker Application Container Engine.
Oct 09 15:25:44 localhost.localdomain dockerd[1916]: time="2021-10-09T15:25:44.195084106+08:00" level=info msg="API listen on /var/ru....sock"
Hint: Some lines were ellipsized, use -l to show in full.
[root@localhost ~]# docker -v
Docker version 19.03.6, build 369ce74a3c
[root@localhost ~]# docker info

```

### 调整镜像仓库

修改docker的registry  
修改/etc/docker目录下的daemon.json文件

在文件中加入

```auto
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
 


```

保存退出

重新启动docker

```auto
chmod +x /etc/systemd/system/docker.service  #添加文件权限并启动docker

 

systemctl daemon-reload               #重载unit配置文件

systemctl start docker     #启动Docker

systemctl restart docker     #重新启动Docker



systemctl enable docker.service       #设置开机自启
```

```auto
[root@localhost ~]# vi /etc/systemd/system/docker.service
[root@localhost ~]# chmod +x /etc/systemd/system/docker.service
[root@localhost ~]# systemctl daemon-reload
[root@localhost ~]# systemctl start docker
[root@localhost ~]# systemctl enable docker.service
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /etc/systemd/system/docker.service.

```

发现内网的环境， 改成了阿里云的，但是没有啥用

```auto
[root@localhost ~]# cat /etc/docker/daemon.json
{
  "registry-mirrors": ["https://ku39pxyp.mirror.aliyuncs.com"],
  "insecure-registries": ["hub.company.com"]
}


```

确保镜像仓库可以ping通

```auto
[root@localhost ~]# curl https://ku39pxyp.mirror.aliyuncs.com
curl: (6) Could not resolve host: ku39pxyp.mirror.aliyuncs.com; Unknown error

[root@localhost ~]# ping ku39pxyp.mirror.aliyuncs.com
ping: ku39pxyp.mirror.aliyuncs.com: Name or service not known
```

### 查看docker info 的引擎信息

```auto
[root@localhost ~]# docker info
Client:
 Debug Mode: false

Server:
 Containers: 14
  Running: 7
  Paused: 0
  Stopped: 7
 Images: 19
 Server Version: 19.03.6
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: b34a5c8af56e510852c35414db4c1f4fa6172339
 runc version: 3e425f80a8c931f88e6d94a8c831b9d5aa481657
 init version: fec3683
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 3.10.0-1062.el7.x86_64
 Operating System: CentOS Linux 7 (Core)
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 15.49GiB
 Name: localhost.localdomain
 ID: I5KF:Y5JA:VCWG:DJYG:PGZO:PZVA:FYXQ:F624:RWH6:4S6R:BI6Z:L2MT
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  hub.gsafety.com
  127.0.0.0/8
 Registry Mirrors:
  https://ku39pxyp.mirror.aliyuncs.com/
 Live Restore Enabled: false




```

### 查看docker相关的进程

```auto
[root@localhost ~]# ps -ef | grep docker
root       1460      1  0 Jun23 ?        04:45:43 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
root       2249   1460  0 Jun23 ?        00:00:09 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 5433 -container-ip 172.26.0.2 -container-port 5432
root       2280   1460  0 Jun23 ?        00:00:09 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 5432 -container-ip 172.26.0.3 -container-port 5432
root       2310   1455  0 Jun23 ?        00:09:35 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/78dc6aacc7d9490fa7c7252dd6b4df01af3b68c2adb69767fb0d51974ea0728c -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root       2311   1455  0 Jun23 ?        00:16:19 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/d6ec26035ca0428d5c3bd1cc154a76b356cf3a7d0746b0455d81223c7b9ab7fd -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root       2483   1460  0 Jun23 ?        00:00:32 /usr/bin/docker-proxy -proto tcp -host-ip 127.0.0.1 -host-port 1514 -container-ip 172.21.0.4 -container-port 10514
root       2538   1455  0 Jun23 ?        02:25:41 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/98500167fb283c56fd43f42d3357c52b393481fdcca2bc7a87128ac35e19fa5a -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root       2571   1455  0 Jun23 ?        02:17:17 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/412652067b159ca617625c315940ce6865534e80fa94b93ef3174f653d21b826 -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root       7077   1460  0 Jun23 ?        00:00:09 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 3306 -container-ip 172.19.0.2 -container-port 3306
root       7085   1455  0 Jun23 ?        00:09:39 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/976bb8cd43729535a74d1583a758be937b6cf8f7a3329a1737fcb722576d1fea -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root       7354   1460  0 Jun23 ?        00:00:09 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 3308 -container-ip 172.19.0.3 -container-port 3306
root       7386   1455  0 Jun23 ?        00:09:45 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/14112371b62521a9b52968a6b0d275700343afeceaac478cfb7a90241dfcdf61 -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root       7402   1460  0 Jun23 ?        00:00:09 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 3307 -container-ip 172.19.0.4 -container-port 3306
root       7431   1455  0 Jun23 ?        00:10:30 containerd-shim -namespace moby -workdir /var/lib/containerd/io.containerd.runtime.v1.linux/moby/a0c6a5d5f891d293ae19e0bc3413729ac41cf38cc7e58d5a547b0f0df87fd6c4 -address /run/containerd/containerd.sock -containerd-binary /usr/bin/containerd -runtime-root /var/run/docker/runtime-runc
root      28336  21582  0 15:32 pts/0    00:00:00 grep --color=auto docker
```

## Harbor概述(开源的镜像仓库)

```html
Habor是由VMWare公司开源的容器镜像仓库。
事实上，Habor是在Docker Registry上进行了相应的
企业级扩展，从而获得了更加广泛的应用，这些新的企业级特性包括：管理用户界面，基于角色的访
问控制 ，AD/LDAP集成以及审计日志等，足以满足基本企业需求。
官方地址：https://vmware.github.io/harbor/cn/

```

### 1、什么是Harbor

• Harbor是VMware公司开源的企业级Docker Registry项目，其目标是帮助用户迅速搭建一个企业级的Docker Registry服务

• Harbor以 Docker 公司开源的Registry 为基础，提供了图形管理UI、基于角色的访问控制(Role Based AccessControl)、AD/LDAP集成、以及审计日志(Auditlogging)等企业用户需求的功能，同时还原生支持中文

• Harbor的每个组件都是以Docker 容器的形式构建的，使用docker-compose 来对它进行部署。用于部署Harbor 的docker- compose模板位于harbor/ docker- compose.yml

### 2、Harbor的特性

1.基于角色控制: 用户和仓库都是基于项目进行组织的，而用户在项目中可以拥有不同的权限

2.基于镜像的复制策略: 镜像可以在多个Harbor实例之间进行复制(同步)

3.支持LDAP/AD: Harbor 可以集成企业内部有的AD/LDAP (类似数据库的一-张表)，用于对已经存在的用户认证和管理

4.镜像删除和垃圾回收: 镜像可以被删除，也可以回收镜像占用的空间

5.图形化用户界面: 用户可以通过浏览器来浏览，搜索镜像仓库以及对项目进行管理

6.审计管理: 所有针对镜像仓库的操作都可以被记录追溯，用于审计管理

7.支持RESTful API: RESTful API提供给管理员对于Harbor 更多的操控，使得与其它管理软件集成变得更容易

8.Harbor 和docker registry的 关系: Harbor实质 上是对docker registry做 了封装，扩展了自己的业务模板

### 3、Harbor的构成

Harbor在架构上主要有Proxy、 Registry、 Core services、 Database (Harbor-db) 、Log collector ( Harbor-log)、Job services六个组件

● Proxy: Harbor 的Registry、 UI、Token 服务等组件，都处在nginx 反向代理后边。该代理将来自浏览器、docker clients的请求转发到后端不同的服务上

● Registry:负责储存Docker 镜像，并处理Docker push/pull命令。由于要对用户进行访问控制，即不同用户对Docker 镜像有不同的读写权限，Registry 会指向一个Token 服务，强制用户的每次Docker pull/push 请求都要携带一个合法的Token,Registry会通过公钥对Token进行解密验证

● Core services: Harbor的核心功能，主要提供以下3个服务:  
1.UI (harbor-ui) :提供图形化界面，帮助用户管理Registry. 上的镜像( image)，并对用户进行授权  
2.WebHook: 为了及时获取Registry.上image 状态变化的情况，在Registry. 上配置 Webhook，把状态变化传递给UI模块  
3.Token 服务:负责根据用户权限给每个Docker push/pull 命令签发Token。 Docker 客户端向Registry服务发起的请求，  
如果不包含Token，会被重定向到Token服务，获得Token后再重新向Registry 进行请求

● Database (harbor-db) :为core services提供数据库服务，负责储存用户权限、审计日志、Docker 镜像分组信息等数据

● Job services: 主要用于镜像复制，本地镜像可以被同步到远程Harbor 实例上

● Log collector (harbor-log) :负责收集其他组件的日志到一个地方

• Harbor的每个组件都是以Docker 容器的形式构建的，因此，使用Docker Compose 来对它进行部署。

• 总共分为7个容器运行，通过在docker-compose.yml所在目录中执行docker-compose ps命令来查看，  
名称分别为: nginx、 harbor-jobservice、 harbor-ui、 harbor-db、harbor-adminserver、registry、 harbor-log.  
其中harbor-adminserver主要是作为一个后端的配置数据管理，并没有太多的其他功能。harbor-ui所要操作的所有数据都通过harbor-adminserver这样一个数据配置管理中心来完成。

![docker 镜像仓库Harbor_Harbor](https://img-blog.csdnimg.cn/img_convert/ee38b5bd08545131ccf2d244d1a6e824.png)

###Docker本地镜像载入与载出

#### 两种办法

+   保存镜像（保存镜像载入后获得跟原镜像id相同的镜像）
+   保存容器（保存容器载入后获得跟原镜像id不同的镜像）

#### **拉取镜像**

通过命令可以从镜像仓库中拉取镜像，默认从[Docker Hub](https://hub.docker.com/) 获取。

命令格式：

docker image pull :

docker image pull rancher/rke-tools:v0.1.52

\[rancher/rke-tools:v0.1.52

#### 保存镜像

+   docker save 镜像id -o /home/mysql.tar
+   docker save 镜像id > /home/mysql.tar

docker save docker.io/rancher/rancher-agent -o /home/rancher-agent .tar

docker save f29ece87a195 -o /home/rancher-agent.tar

docker save docker.io/rancher/rke-tools -o /home/rke-tools-v0.1.52.tar

#### 载入镜像

+   docker load -i mysql.tar

docker load -i /usr/local/rancher-v2.3.5.tar

docker load -i /usr/local/rancher-agent.tar

docker inspect f29ece87a1954772accb8a2332ee8c3fe460697e3f102ffbdc76eb9bc4f4f1d0

docker load -i /usr/local/rke-tools-v0.1.52.tar

```auto
docker load -i mysql.tar

[root@localhost ~]# docker load -i /usr/local/rancher-v2.3.5.tar
43c67172d1d1: Loading layer [==================================================>]  65.57MB/65.57MB
21ec61b65b20: Loading layer [==================================================>]  991.2kB/991.2kB
1d0dfb259f6a: Loading layer [==================================================>]  15.87kB/15.87kB
f55aa0bd26b8: Loading layer [==================================================>]  3.072kB/3.072kB
e0af200d6950: Loading layer [==================================================>]  126.1MB/126.1MB
088ed892f9ad: Loading layer [==================================================>]  6.656kB/6.656kB
6aa3142b4130: Loading layer [==================================================>]   34.5MB/34.5MB
f4e84c05ab29: Loading layer [==================================================>]  70.41MB/70.41MB
11a6e4332b53: Loading layer [==================================================>]  224.8MB/224.8MB
46d1ac556da7: Loading layer [==================================================>]  3.072kB/3.072kB
0f8b224a5802: Loading layer [==================================================>]  57.87MB/57.87MB
519eba7d586a: Loading layer [==================================================>]  99.58MB/99.58MB
3f8bb7c0c150: Loading layer [==================================================>]  4.608kB/4.608kB
c22c9a5a8211: Loading layer [==================================================>]  3.072kB/3.072kB
Loaded image: rancher/rancher:v2.3.5

```

#### 打个tag

docker tag f29ece87a1954772accb8a2332ee8c3fe460697e3f102ffbdc76eb9bc4f4f1d0 rancher/rancher-agent:v2.3.5

docker tag f29ece87a195 172.18.8.104/rancher/rancher-agent:v2.3.5

docker tag 6e421b8753a2 172.18.8.104/rancher/rke-tools:v0.1.52

83fe4871cf67

docker rmi image\_name

docker rmi -f 172.18.8.104/rancher/coredns-coredns:1.6.5

docker rmi -f 172.18.8.104/rancher/coredns-coredns:v3.4.3-rancher1

docker rmi [hub.doge.net/ubuntu:latest](http://hub.doge.net/ubuntu:latest)

#### 保存镜像

+   docker export 镜像id -o /home/mysql-export.tar
+   docker save 镜像tag -o /home/mysql-export.tar

#### 载入镜像

+   docker import mysql-export.tar

### Docker本地容器相关的操作

#### 创建容器

创建名为"centos6"的容器，并在容器内部和宿主机中查看容器中的进程信息

```auto
 docker run -itd -p 6080:80 -p 6022:22 docker.io/lemonbar/centos6-ssh:latest
```

结果如下

```auto
[root@VM-4-17-centos ~]#    docker run -itd -p 80:80 -p 6022:22 docker.io/lemonbar/centos6-ssh:latest
Unable to find image 'lemonbar/centos6-ssh:latest' locally
latest: Pulling from lemonbar/centos6-ssh
a3ed95caeb02: Pull complete
f79eb1f22352: Pull complete
67c1aaa530c8: Pull complete
80447774eee7: Pull complete
6d67b3a80e5a: Pull complete
f1819e4b2f8f: Pull complete
09712b5b9acc: Pull complete
8bc987c5494f: Pull complete
c42b021d0ff2: Pull complete
Digest: sha256:093c2165b3c6fe05d5658343456f9b59bb7ecc690a7d3a112641c86083227dd1
Status: Downloaded newer image for lemonbar/centos6-ssh:latest
a4f1c9b8abcda78c8764cc285183dfa56cd1aa4ce6d111d4d9e77f3a57f3d5fc


```

#### 查看活跃容器

docker ps

```auto
CONTAINER ID        IMAGE                                     COMMAND                  CREATED             STATUS                          PORTS                                              NAMES
a4f1c9b8abcd        lemonbar/centos6-ssh:latest               "/bin/sh -c '/usr/sb…"   32 seconds ago      Up 31 seconds                   0.0.0.0:6022->22/tcp, 0.0.0.0:6080->80/tcp         determined_curie

```

#### 查看全部容器

docker ps -a

#### 停止容器

docker stop id

#### 删除容器

docker rm id

#### 查看容器的进程信息

\*\*docker top 😗\*查看容器中运行的进程信息，支持 ps 命令参数。

语法

```auto
docker top [OPTIONS] CONTAINER [ps OPTIONS]
```

容器运行时不一定有/bin/bash终端来交互执行top命令，而且容器还不一定有top命令，可以使用docker top来实现查看container中正在运行的进程。

从[Docker 1.11](https://github.com/docker/docker/releases/tag/v1.11.1)开始，Docker容器运行已经不是简单的通过Docker daemon来启动，而是集成了containerd、runC等多个组件。Docker服务启动之后，我们也可以看见系统上启动了dockerd、docker-containerd等进程，本文主要介绍新版Docker（1.11以后）每个部分的功能和作用。

#### 查找容器名称的命令

```auto
[root@localhost ~]# docker ps --format "{{.Names}}"
```

结果如下：

```auto
[root@VM-4-17-centos ~]# docker ps --format "{{.Names}}"
determined_curie
redis
nginx_slave
nginx_master
nginx_empty
loving_agnesi
pxc_proxy
pxc03
pxc02
pxc01
affectionate_austin
nostalgic_blackwell

```

### 在容器内部和宿主机中查看容器中的进程信息

```auto
docker exec -it determined_curie  ps -ef
```

结果如下：

```auto
[root@VM-4-17-centos ~]# docker exec -it determined_curie  ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 08:14 pts/0    00:00:00 /usr/sbin/sshd -D
root         5     0  0 08:16 pts/1    00:00:00 ps -ef

```

我们可以使用`docker exec`命令进入容器PID名空间，并执行应用。

通过`ps -ef`命令，可以看到每个determined\_curie 容器都包含一个PID为1的进程，

“/usr/sbin/sshd”，它是容器的启动进程，具有特殊意义。

利用`docker top`命令，可以让我们从宿主机操作系统中看到容器的进程信息。

```auto
[root@VM-4-17-centos ~]# docker top determined_curie
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                27880               27866               0                   16:14               pts/0               00:00:00            /usr/sbin/sshd -D
[root@VM-4-17-centos ~]#

```

#### 查看其父进程信息

```auto
[root@VM-4-17-centos ~]#  ps aux | grep 4948
root     17205  1414  0 16:37 pts/0    00:00:00 grep --color=auto 27866
root     27866  5587  0 16:14 ?        00:00:00 docker-containerd-shim -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/a4f1c9b8abcda78c8764cc285183dfa56cd1aa4ce6d111d4d9e77f3a57f3d5fc -address /var/run/docker/containerd/docker-containerd.sock -containerd-binary /usr/bin/docker-containerd -runtime-root /var/run/docker/runtime-runc
root     27880 27866  0 16:14 pts/0    00:00:00 /usr/sbin/sshd -D

```

#### 查看子进程信息

```auto
[root@VM-4-17-centos ~]#  ps aux | grep 27880
root     17777  0.0  0.0 115928  1008 pts/0    S+   16:38   0:00 grep --color=auto 27880
root     27880  0.0  0.0  66664  3072 pts/0    Ss+  16:14   0:00 /usr/sbin/sshd -D

```

#### 总计三个命令

```auto
ps -ef | grep 4948 #查看父进程
ps aux | grep 27880 #查看子进程(容器)
docker ps -a | grep determined_curie   #定位容器id

```

### 再启动一个 centos 容器

```auto
 docker run -itd  --name centos6-2  -p 6081:80 -p 6021:22 docker.io/lemonbar/centos6-ssh:latest
```

输出如下：

```auto
[root@VM-4-17-centos ~]# docker run -itd  --name centos6-2  -p 6081:80 -p 6021:22 docker.io/lemonbar/centos6-ssh:latest
460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd

```

#### 查看进程信息

利用`docker top`命令，可以让我们从宿主机操作系统中看到容器的进程信息。

```auto
[root@VM-4-17-centos ~]# docker top centos6-2
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                4962                4948                0                   16:24               pts/0               00:00:00            /usr/sbin/sshd -D


```

#### 查看其父进程信息

```auto
[root@VM-4-17-centos ~]# ps -ef | grep 4948
root      4948  5587  0 16:24 ?        00:00:00 docker-containerd-shim -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd -address /var/run/docker/containerd/docker-containerd.sock -containerd-binary /usr/bin/docker-containerd -runtime-root /var/run/docker/runtime-runc
root      4962  4948  0 16:24 pts/0    00:00:00 /usr/sbin/sshd -D

```

#### 查看子进程信息

```auto
[root@VM-4-17-centos ~]# ps aux | grep 4962
root      4962  0.0  0.0  66664  3068 pts/0    Ss+  16:24   0:00 /usr/sbin/sshd -D
root     15311  0.0  0.0 115932  1008 pts/0    S+   16:35   0:00 grep --color=auto 4962
```

#### 总计三个命令

```auto
ps -ef | grep 4948 #查看父进程
ps aux | grep 4962 #查看子进程(容器)
docker ps -a | grep centos6-2  #定位容器id

```

### 进程的对应关系

#### Linux通过进程ID查看文件路径

子进程的文件路径

```auto
[root@VM-4-17-centos ~]#  ls -l /proc/27880
total 0
dr-xr-xr-x 2 root root 0 Nov  3 16:41 attr
-rw-r--r-- 1 root root 0 Nov  3 16:41 autogroup
-r-------- 1 root root 0 Nov  3 16:41 auxv
-r--r--r-- 1 root root 0 Nov  3 16:14 cgroup
--w------- 1 root root 0 Nov  3 16:41 clear_refs
-r--r--r-- 1 root root 0 Nov  3 16:15 cmdline
-rw-r--r-- 1 root root 0 Nov  3 16:41 comm
-rw-r--r-- 1 root root 0 Nov  3 16:41 coredump_filter
-r--r--r-- 1 root root 0 Nov  3 16:41 cpuset
lrwxrwxrwx 1 root root 0 Nov  3 16:41 cwd -> /
-r-------- 1 root root 0 Nov  3 16:41 environ
lrwxrwxrwx 1 root root 0 Nov  3 16:14 exe -> /usr/sbin/sshd
dr-x------ 2 root root 0 Nov  3 16:14 fd
dr-x------ 2 root root 0 Nov  3 16:41 fdinfo
-rw-r--r-- 1 root root 0 Nov  3 16:41 gid_map
-r-------- 1 root root 0 Nov  3 16:41 io
-r--r--r-- 1 root root 0 Nov  3 16:41 limits
-rw-r--r-- 1 root root 0 Nov  3 16:41 loginuid
dr-x------ 2 root root 0 Nov  3 16:41 map_files
-r--r--r-- 1 root root 0 Nov  3 16:41 maps
-rw------- 1 root root 0 Nov  3 16:41 mem
-r--r--r-- 1 root root 0 Nov  3 16:14 mountinfo
-r--r--r-- 1 root root 0 Nov  3 16:41 mounts
-r-------- 1 root root 0 Nov  3 16:41 mountstats
dr-xr-xr-x 5 root root 0 Nov  3 16:41 net
dr-x--x--x 2 root root 0 Nov  3 16:14 ns
-r--r--r-- 1 root root 0 Nov  3 16:41 numa_maps
-rw-r--r-- 1 root root 0 Nov  3 16:41 oom_adj
-r--r--r-- 1 root root 0 Nov  3 16:41 oom_score
-rw-r--r-- 1 root root 0 Nov  3 16:41 oom_score_adj
-r--r--r-- 1 root root 0 Nov  3 16:41 pagemap
-r-------- 1 root root 0 Nov  3 16:41 patch_state
-r--r--r-- 1 root root 0 Nov  3 16:41 personality
-rw-r--r-- 1 root root 0 Nov  3 16:41 projid_map
lrwxrwxrwx 1 root root 0 Nov  3 16:41 root -> /
-rw-r--r-- 1 root root 0 Nov  3 16:41 sched
-r--r--r-- 1 root root 0 Nov  3 16:41 schedstat
-r--r--r-- 1 root root 0 Nov  3 16:41 sessionid
-rw-r--r-- 1 root root 0 Nov  3 16:41 setgroups
-r--r--r-- 1 root root 0 Nov  3 16:41 smaps
-r--r--r-- 1 root root 0 Nov  3 16:41 stack
-r--r--r-- 1 root root 0 Nov  3 16:14 stat
-r--r--r-- 1 root root 0 Nov  3 16:41 statm
-r--r--r-- 1 root root 0 Nov  3 16:14 status
-r--r--r-- 1 root root 0 Nov  3 16:41 syscall
dr-xr-xr-x 3 root root 0 Nov  3 16:41 task
-r--r--r-- 1 root root 0 Nov  3 16:41 timers
-rw-r--r-- 1 root root 0 Nov  3 16:14 uid_map
-r--r--r-- 1 root root 0 Nov  3 16:41 wchan

```

以下是/proc目录中进程27880的信息说明：

```auto
proc/27880 pid为N的进程信息

/proc/27880/cmdline 进程启动命令

/proc/27880/cwd 链接到进程当前工作目录

/proc/27880/environ 进程环境变量列表

/proc/27880/exe 链接到进程的执行命令文件

/proc/27880/fd 包含进程相关的所有的文件描述符

/proc/27880/maps 与进程相关的内存映射信息

/proc/27880/mem 指代进程持有的内存，不可读

/proc/27880/root 链接到进程的根目录

/proc/27880/stat 进程的状态

/proc/27880/statm 进程使用的内存的状态

/proc/27880/status 进程状态信息，比stat/statm更具可读性
```

#### 容器的PID namespace（命名空间）

在Docker中，进程管理的基础就是Linux内核中的PID名空间技术。

在不同PID名空间中，进程ID是独立的；即在两个不同名空间下的进程可以有相同的PID。

在Docker中，每个Container进程缺省都具有不同的PID名空间。通过名空间技术，Docker实现容器间的进程隔离。

docker中运行的容器进程，本质上还是运行在宿主机上的，所以也会拥有相对应的PID

##### 找出容器ID

```auto
# docker ps
```

输出

```auto
[root@VM-4-17-centos ~]# docker ps
CONTAINER ID        IMAGE                                     COMMAND                  CREATED             STATUS                          PORTS                                              NAMES
460d68823930        lemonbar/centos6-ssh:latest               "/bin/sh -c '/usr/sb…"   32 minutes ago      Up 32 minutes                   0.0.0.0:6021->22/tcp, 0.0.0.0:6081->80/tcp         centos6-2

```

#### 查看容器信息

```auto
docker inspect  id
```

输出

```auto
[root@VM-4-17-centos ~]# docker inspect  460d68823930
[root@VM-4-17-centos ~]#  docker inspect  460d68823930
[
    {
        "Id": "460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd",
        "Created": "2021-11-03T08:24:36.934129599Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "/usr/sbin/sshd -D"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 4962,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-11-03T08:24:37.223255812Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:efd998bd6817af509d348b488e3ce4259f9f05632644a7bf574b785bbc8950b8",
        "ResolvConfPath": "/var/lib/docker/containers/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd/hostname",
        "HostsPath": "/var/lib/docker/containers/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd/hosts",
        "LogPath": "/var/lib/docker/containers/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd-json.log",
        "Name": "/centos6-2",
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
            "PortBindings": {
                "22/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "6021"
                    }
                ],
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "6081"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "shareable",
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
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/6835c1b48237aafe27e2efabeda92a3a6623f254f88d54b5e6acce454e560dd6-init/diff:/var/lib/docker/overlay2/7139bf0b716c6e0b6a0c709b7043466f9bbfd7024f8ae584061c00b0bd97348c/diff:/var/lib/docker/overlay2/66a3e278259cdcf50741ce30a115baa3bd6247a60c487e4118e85f2f39328f11/diff:/var/lib/docker/overlay2/20e22c4c28ebadb615eb4c7c290253d3eb91cb49722ee2931b0ee628352a5857/diff:/var/lib/docker/overlay2/a3fa9dbebc83a853083205b8f7921c632cd67f64531f4a25cab419a43172e3ae/diff:/var/lib/docker/overlay2/3af7958c9a4e54d24598058a9fa1e85eb35e3d40f766fa498a674b52724ae73e/diff:/var/lib/docker/overlay2/becb65af4396137ed41fe6d516e834e6e6e9120f4edfac8e2ca8dd67cce23268/diff:/var/lib/docker/overlay2/fef055305158cc96906514c447f0eaea05945138896b0b35ac4146b6a2a3e273/diff:/var/lib/docker/overlay2/79158cdf3ba832493ab0d02d560c784208fe51c74236a5a86f7fb4fb50ab6e44/diff:/var/lib/docker/overlay2/86258a18e1110582b819719593687f11f0404d00a41667b3432c3b974fb1ce42/diff:/var/lib/docker/overlay2/8826b2e0068653fb2c5e8a3dbf839470e2b8eef8cf752b5fe901bea1b210849f/diff:/var/lib/docker/overlay2/145301e2738a8a7581c2bbd5beb9bf7a49b247e46642b8084efbc026a1826116/diff:/var/lib/docker/overlay2/f621f37535e0db1fe44902e22dba7ef0844b9a8b562a9daa39a842a49e9cc9bb/diff:/var/lib/docker/overlay2/7b493e4a97907aaa18b97ad2e9120b5bf87c0e9908ee390a35ea6ff546d8cec6/diff",
                "MergedDir": "/var/lib/docker/overlay2/6835c1b48237aafe27e2efabeda92a3a6623f254f88d54b5e6acce454e560dd6/merged",
                "UpperDir": "/var/lib/docker/overlay2/6835c1b48237aafe27e2efabeda92a3a6623f254f88d54b5e6acce454e560dd6/diff",
                "WorkDir": "/var/lib/docker/overlay2/6835c1b48237aafe27e2efabeda92a3a6623f254f88d54b5e6acce454e560dd6/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "460d68823930",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "22/tcp": {},
                "80/tcp": {}
            },
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": false,
            "Env": [
                "HOME=/",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "/usr/sbin/sshd -D"
            ],
            "Image": "docker.io/lemonbar/centos6-ssh:latest",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "ea66261fb6d8089d5b2d585a2dc32b2003365df7118f5f5e898a152fb5b35773",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "22/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "6021"
                    }
                ],
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "6081"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/ea66261fb6d8",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "09ad719a4e9115ee56c5fb0f5b0d39c50bf5acaf0a1afacedc13969c82a2969f",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.6",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:06",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "2586283d16a08210c955d705f05e0f6999b59523a84b0c163e33f535af809ddd",
                    "EndpointID": "09ad719a4e9115ee56c5fb0f5b0d39c50bf5acaf0a1afacedc13969c82a2969f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.6",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:06",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

#### 进入相应目录

```auto
# cd /sys/fs/cgroup/memory/docker/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd/
```

输出

```auto
 cd /sys/fs/cgroup/memory/docker/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd/
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# ll
total 0
-rw-r--r-- 1 root root 0 Nov  3 16:24 cgroup.clone_children
--w--w--w- 1 root root 0 Nov  3 16:24 cgroup.event_control
-rw-r--r-- 1 root root 0 Nov  3 16:24 cgroup.procs
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.failcnt
--w------- 1 root root 0 Nov  3 16:24 memory.force_empty
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.failcnt
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.limit_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.max_usage_in_bytes
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.slabinfo
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.tcp.failcnt
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.tcp.limit_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.tcp.max_usage_in_bytes
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.tcp.usage_in_bytes
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.kmem.usage_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.limit_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.max_usage_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.memsw.failcnt
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.memsw.limit_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.memsw.max_usage_in_bytes
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.memsw.usage_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.move_charge_at_immigrate
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.numa_stat
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.oom_control
---------- 1 root root 0 Nov  3 16:24 memory.pressure_level
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.soft_limit_in_bytes
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.stat
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.swappiness
-r--r--r-- 1 root root 0 Nov  3 16:24 memory.usage_in_bytes
-rw-r--r-- 1 root root 0 Nov  3 16:24 memory.use_hierarchy
-rw-r--r-- 1 root root 0 Nov  3 16:24 notify_on_release
-rw-r--r-- 1 root root 0 Nov  3 16:24 tasks

```

```auto
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# cat cgroup.procs
4962
11539
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# cat pids.max
max
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# cat tasks
4962
11539
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# cat cgroup.clone_children
0
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# pwd
/sys/fs/cgroup/pids/docker/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd

```

#### 查看容器目录里的进程号

进程号就存在一个文件里面

```auto
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# 
cat cgroup.procs
4962

```

与前面利用`docker top`命令，可以让我们从宿主机操作系统中看到容器的进程信息。

```auto
[root@VM-4-17-centos ~]# docker top centos6-2
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                4962                4948                0                   16:24               pts/0               00:00:00            /usr/sbin/sshd -D


```

#### 启动一个进程

我们下面会在 centos6-2容器中，利用`docker exec`命令启动一个"sleep"进程

```auto
[root@VM-4-17-centos ]# docker exec -d  centos6-2  sleep 2000
[root@VM-4-17-centos ]# docker exec  centos6-2  ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 08:24 pts/0    00:00:00 /usr/sbin/sshd -D
root         6     0  0 09:06 ?        00:00:00 sleep 2000
root        10     0  0 09:06 ?        00:00:00 ps -ef


```

查看宿主机的进程号

```auto
[root@VM-4-17-centos ]#  docker top centos6-2
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                4962                4948                0                   16:24               pts/0               00:00:00            /usr/sbin/sshd -D
root                11539               4948                0                   17:06               ?                   00:00:00            sleep 2000

```

我们可以清楚的看到exec命令创建的sleep进程属 centos6-2 容器的名空间，但是它的父进程是Docker 容器的启动进程。

#### 查看容器目录里的进程号

进程号就存在一个文件里面

```auto
[root@VM-4-17-centos 460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd]# cat cgroup.procs
4962
11539


```

```auto
 docker exec -d  centos6-2 pstree -p
 
 docker exec -d  centos6-2 ps -auxf
 
  docker exec -d  centos6-2 ll /proc
```

输出

```auto
[root@VM-4-17-centos docker]#  docker exec  centos6-2  ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 08:24 pts/0    00:00:00 /usr/sbin/sshd -D
root         6     0  0 09:06 ?        00:00:00 sleep 2000
root        40     0  0 09:26 ?        00:00:00 ps -ef
[root@VM-4-17-centos docker]#  docker exec  centos6-2  ps -auxf
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        44  0.0  0.0  13360  1012 ?        Rs   09:26   0:00 ps -auxf
root         6  0.0  0.0   4120   316 ?        Ss   09:06   0:00 sleep 2000
root         1  0.0  0.0  66664  3068 pts/0    Ss+  08:24   0:00 /usr/sbin/sshd -D
Warning: bad syntax, perhaps a bogus '-'? See /usr/share/doc/procps-3.2.8/FAQ
[root@VM-4-17-centos docker]#  docker exec  centos6-2  pstree -p
sshd(1)

```

## Docker文件目录和容器内部操作

Docker默认的文件目录位于Linux server的/var/lib/docker 下面。目录结构如下

![img](https://img-blog.csdnimg.cn/img_convert/478405e24eeb0ddeb907ef771dffface.png)

|-----containers：用于存储容器信息

|-----image：用来存储镜像中间件及本身信息，大小，依赖信息

|-----network

|-----swarm

|-----tmp：docker临时目录

|-----trust：docker信任目录

|-----volumes：docker卷目录

还可以通过docker指令确认文件位置：

```auto
docker info
```

![img](https://img-blog.csdnimg.cn/img_convert/c8653ab0fa9f53f96f7e9982f3494e90.png)

查看某个容器的文件目录：

```auto
 docker exec 容器name ls
```

![img](https://img-blog.csdnimg.cn/img_convert/c7bd6c11889b4b0af706318b61c7d549.png)

```auto
 docker exec centos6-2   ls /proc
```

```auto
[root@VM-4-17-centos containers]#  docker exec centos6-2  ls /proc
1
103
acpi
buddyinfo
bus
cgroups
cmdline
consoles
cpuinfo
crypto
devices
diskstats
dma
driver
execdomains
fb
filesystems
fs
interrupts
iomem
ioports
irq
kallsyms
kcore
key-users
keys
kmsg
kpagecount
kpageflags
loadavg
locks
mdstat
meminfo
misc
modules
mounts
mtrr
net
pagetypeinfo
partitions
sched_debug
schedstat
scsi
self
slabinfo
softirqs
stat
swaps
sys
sysrq-trigger
sysvipc
timer_list
timer_stats
tty
uptime
version
vmallocinfo
vmstat
zoneinfo

```

## docker daemon (docker守护进程)

```auto
pidof dockerd   #查看docker守护进程pid
lsof -p 3197 | wc -l #docker守护进程打开的文件数
```

在两个容器中的"centos "是两个独立的进程，但是他们拥有相同的父进程 Docker Daemon。

所以Docker可以父子进程的方式在Docker Daemon和Redis容器之间进行交互。

另一个值得注意的方面是，`docker exec`命令可以进入指定的容器内部执行命令。由它启动的进程属于容器的namespace和相应的cgroup。

但是这些进程的父进程是Docker Daemon而非容器的PID1进程。

我们下面会在Redis容器中，利用`docker exec`命令启动一个"sleep"进程

```auto
docker@default:~$ docker exec -d redis sleep 2000
docker@default:~$ docker exec redis ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
redis        1     0  0 02:26 ?        00:00:00 redis-server *:6379
root        11     0  0 02:26 ?        00:00:00 sleep 2000
root        21     0  0 02:29 ?        00:00:00 ps -ef
docker@default:~$ docker top redis
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
999                 9955                1264                0                   02:12               ?                   00:00:00            redis-server *:6379
root                9984                1264                0                   02:13               ?                   00:00:00            sleep 2000
```

我们可以清楚的看到exec命令创建的sleep进程属Redis容器的名空间，但是它的父进程是Docker Daemon。

如果我们在宿主机操作系统中手动杀掉容器的启动进程（在上文示例中是redis-server），容器会自动结束，而容器名空间中所有进程也会退出。

```auto
docker@default:~$ PID=$(docker inspect --format="{{.State.Pid}}" redis)
docker@default:~$ sudo kill $PID
docker@default:~$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
356eca186321        redis               "/entrypoint.sh redis"   23 minutes ago      Up 4 minutes               6379/tcp            redis2
f6bc57cc1b46        redis               "/entrypoint.sh redis"   23 minutes ago      Exited (0) 4 seconds ago                       redis
```

通过以上示例：

+   每个容器有独立的PID名空间，
+   容器的生命周期和其PID1进程一致
+   利用`docker exec`可以进入到容器的名空间中启动进程

## Docker Daemon 原理

作为Docker容器管理的守护进程，Docker Daemon从最初集成在`docker`命令中（1.11版本前），到后来的独立成单独二进制程序（1.11版本开始），其功能正在逐渐拆分细化，被分配到各个单独的模块中去。

### 演进：Docker守护进程启动

从Docker服务的启动脚本，也能看见守护进程的逐渐剥离：

在Docker 1.8之前，Docker守护进程启动的命令为：

```shell
docker -d
```

这个阶段，守护进程看上去只是Docker client的一个选项。

Docker 1.8开始，启动命令变成了：

```shell
docker daemon
```

这个阶段，守护进程看上去是`docker`命令的一个模块。

Docker 1.11开始，守护进程启动命令变成了：

```shell
dockerd
```

其服务的配置文件为：

```auto

[Service]
Type=notify
# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID
```

此时已经和Docker client分离，独立成一个二进制程序了。

当然，守护进程模块不停的在重构，其基本功能和定位没有变化。和一般的CS架构系统一样，守护进程负责和Docker client交互，并管理Docker镜像、容器。

### OCI（Open Container Initiative）

Open Container Initiative，也就是常说的OCI，是由多家公司共同成立的项目，并由linux基金会进行管理，致力于container runtime的标准的制定和runc的开发等工作。  
官方的介绍是

> An open governance structure for the express purpose of creating open industry standards around container formats and runtime. – Open Containers Official Site

所谓container runtime，主要负责的是容器的生命周期的管理。oci的runtime spec标准中对于容器的状态描述，以及对于容器的创建、删除、查看等操作进行了定义。

目前主要有两个标准文档：容器运行时标准 （runtime spec）和 容器镜像标准（image spec）。  
这两个协议通过 OCI runtime filesytem bundle 的标准格式连接在一起，OCI 镜像可以通过工具转换成 bundle，然后 OCI 容器引擎能够识别这个 bundle 来运行容器。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411054154638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)

#### image spec

OCI 容器镜像主要包括几块内容：

文件系统：以 layer 保存的文件系统，每个 layer 保存了和上层之间变化的部分，layer 应该保存哪些文件，怎么表示增加、修改和删除的文件等  
config 文件：保存了文件系统的层级信息（每个层级的 hash 值，以及历史信息），以及容器运行时需要的一些信息（比如环境变量、工作目录、命令参数、mount 列表），指定了镜像在某个特定平台和系统的配置。比较接近我们使用 docker inspect <image\_id> 看到的内容  
manifest 文件：镜像的 config 文件索引，有哪些 layer，额外的 annotation 信息，manifest 文件中保存了很多和当前平台有关的信息  
index 文件：可选的文件，指向不同平台的 manifest 文件，这个文件能保证一个镜像可以跨平台使用，每个平台拥有不同的 manifest 文件，使用 index 作为索引

#### runtime spec

OCI 对容器 runtime 的标准主要是指定容器的运行状态，和 runtime 需要提供的命令。下图可以是容器状态转换图：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411054321900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)

### Docker CLI

```auto
/usr/bin/docker
```

Docker 的客户端工具，通过CLI与 dockerd API 交流。 CLI 的例子比如docker build … docker run …

### Docker Daemon

```auto
/usr/bin/dockerd
```

当然，守护进程模块不停的在重构，其基本功能和定位没有变化。和一般的CS架构系统一样，守护进程负责和Docker client交互，并管理Docker镜像、容器。

### Containerd

```auto
/usr/bin/docker-containerd
```

containerd是容器技术标准化之后的产物，为了能够兼容OCI标准，将容器运行时及其管理功能从Docker Daemon剥离。理论上，即使不运行dockerd，也能够直接通过containerd来管理容器。（当然，containerd本身也只是一个守护进程，容器的实际运行时由后面介绍的runC控制。）  
最近，Docker刚刚宣布开源containerd。从其项目介绍页面可以看出，containerd主要职责是**镜像管理**（镜像、元信息等）、**容器执行**（调用最终运行时组件执行）。

containerd向上为Docker Daemon提供了gRPC接口，使得Docker Daemon屏蔽下面的结构变化，确保原有接口向下兼容。向下通过containerd-shim结合runC，使得引擎可以独立升级，避免之前Docker Daemon升级会导致所有容器不可用的问题。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411060507409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411162646910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)  
containerd fully leverages the **OCI runtime specification1, image format specifications and OCI reference implementation (runc)**.  
containerd includes a daemon exposing gRPC API over a local UNIX socket. The API is a low-level one designed for higher layers to wrap and extend. Containerd uses RunC to run containers according to the OCI specification.

### docker-shim

```auto
/usr/bin/docker-containerd-shim
```

每启动一个容器都会起一个新的docker-shim的一个进程.  
他直接通过指定的三个参数来创建一个容器：

1.  容器id
2.  boundle目录（containerd的对应某个容器生成的目录，一般位于：/var/run/docker/libcontainerd/containerID）
3.  运行是二进制（默认为runc）来调用runc的api（比如创建容器时，最后拼装的命令如下：runc create 。。。）

他的作用是：

1.  它允许容器运行时(即 runC)在启动容器之后退出，简单说就是不必为每个容器一直运行一个容器运行时(runC)
2.  即使在 containerd 和 dockerd 都挂掉的情况下，容器的标准 IO 和其它的文件描述符也都是可用的
3.  向 containerd 报告容器的退出状态  
    前两点尤其重要，有了它们就可以在不中断容器运行的情况下升级或重启 dockerd(这对于生产环境来说意义重大)。

### runc (OCI reference implementation)

```auto
/usr/bin/docker-runc 
```

OCI定义了容器运行时标准OCI Runtime Spec support (aka runC)，runC是Docker按照开放容器格式标准（OCF, Open Container Format）制定的一种具体实现。

runC是从Docker的**libcontainer**中迁移而来的，实现了容器启停、资源隔离等功能。

Docker默认提供了docker-runc实现，事实上，通过containerd的封装，可以在Docker Daemon启动的时候指定runc的实现。

我们可以通过启动Docker Daemon时增加–add-runtime参数来选择其他的runC现。例如：

```auto
docker daemon --add-runtime "custom=/usr/local/bin/my-runc-replacement"
```

### Docker、containerd, containerd-shim和runc之间的关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411053950473.png)  
他们之间的关系如下图：

![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMTA4MTIxNDUyMzc0?x-oss-process=image/format,png)

我们可以通过启动一个Docker容器，来观察进程之间的关联。

### 通过docker 而通过runc来启动一个container的过程

#### 查看进程信息

利用`docker top`命令，可以让我们从宿主机操作系统中看到容器的进程信息。

```auto
[root@VM-4-17-centos ~]# docker top centos6-2
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                4962                4948                0                   16:24               pts/0               00:00:00            /usr/sbin/sshd -D


```

#### 查看子进程信息

```auto

[root@VM-4-17-centos containerd]# ps aux | grep 4948
root      4948  0.0  0.0  12212  3696 ?        Sl   16:24   0:00 docker-containerd-shim -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd -address /var/run/docker/containerd/docker-containerd.sock -containerd-binary /usr/bin/docker-containerd -runtime-root /var/run/docker/runtime-runc
root     27040  0.0  0.0 115932  1004 pts/0    S+   18:32   0:00 grep --color=auto 4948

```

#### 查看进程树

```undefined
pstree -l -a -A 4948 -p

```

输出结果如下：

```auto
[root@VM-4-17-centos containerd]# pstree -l -a -A 4948 -p
docker-containe,4948 -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd -address /var/run/docker/containerd/docker-containerd.sock -containerd-binary /usr/bin/docker-containerd -runtime-root /var/run/docker/runtime-runc
  |-sshd,4962 -D
  |-{docker-containe},4949
  |-{docker-containe},4950
  |-{docker-containe},4951
  |-{docker-containe},4952
  |-{docker-containe},4953
  |-{docker-containe},4954
  `-{docker-containe},1593


```

虽然`pstree`命令截断了命令，但我们还是能够看出，

当Docker daemon启动之后，dockerd和docker-containerd进程一直存在。

当启动容器之后，docker-containerd进程（也是这里介绍的containerd组件）会创建docker-containerd-shim进程，其中的参数460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd就是要启动容器的id。

最后docker-containerd-shim子进程，已经是实际在容器中运行的进程（既sleep 1000）。

docker-containerd-shim另一个参数，是一个和容器相关的目录/var/run/docker/containerd/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd，里面的内容有：

```cpp
[root@VM-4-17-centos containerd]# ll /var/run/docker/containerd/460d688239304172f39bb9586bfc5959e0c3db64e7c3a0937f1003f94408ebbd
total 0
prwx------ 1 root root 0 Nov  3 16:24 init-stdin
prwx------ 1 root root 0 Nov  3 16:24 init-stdout

```

其中包括了容器配置和标准输入、标准输出、标准错误三个管道文件。

#### docker-shim

docker-shim是一个真实运行的容器的真实垫片载体，

每启动一个容器都会起一个新的docker-shim的一个进程，

他直接通过指定的三个参数：

+   容器id，

+   boundle目录（containerd的对应某个容器生成的目录，一般位于：/var/run/docker/libcontainerd/containerID），

+   运行时二进制（默认为runc）

    调用runc的api创建一个容器（比如创建容器：最后拼装的命令如下：runc create 。。。。。）


#### RunC

OCI定义了容器运行时标准，

runC是Docker按照开放容器格式标准（OCF, Open Container Format）制定的一种具体实现。

runC是从Docker的libcontainer中迁移而来的，实现了容器启停、资源隔离等功能。

Docker默认提供了docker-runc实现，事实上，通过containerd的封装，可以在Docker Daemon启动的时候指定runc的实现。

### CRI

kubernetes在初期版本里，就对多个容器引擎做了兼容，因此可以使用docker、rkt对容器进行管理。

以docker为例，kubelet中会启动一个docker manager，通过直接调用docker的api进行容器的创建等操作。

在k8s 1.5版本之后，kubernetes推出了自己的运行时接口api–CRI(container runtime interface)。cri接口的推出，隔离了各个容器引擎之间的差异，而通过统一的接口与各个容器引擎之间进行互动。

与oci不同，cri与kubernetes的概念更加贴合，并紧密绑定。

cri不仅定义了容器的生命周期的管理，还引入了k8s中pod的概念，并定义了管理pod的生命周期。

在kubernetes中，pod是由一组进行了资源限制的，在隔离环境中的容器组成。而这个隔离环境，称之为PodSandbox。在cri开始之初，主要是支持docker和rkt两种。其中kubelet是通过cri接口，调用docker-shim，并进一步调用docker api实现的。

如上文所述，docker独立出来了containerd。kubernetes也顺应潮流，孵化了cri-containerd项目，用以将containerd接入到cri的标准中。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411163519809.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411061032726.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190415141804994.png)

为了进一步与oci进行兼容，kubernetes还孵化了cri-o，成为了架设在cri和oci之间的一座桥梁。通过这种方式，可以方便更多符合oci标准的容器运行时，接入kubernetes进行集成使用。可以预见到，通过cri-o，kubernetes在使用的兼容性和广泛性上将会得到进一步加强。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190411061049452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzIxMjIyMTQ5,size_16,color_FFFFFF,t_70)

## docker-compose

Docker-Compose 项目是Docker官方的开源项目，负责实现对Docker容器集群的快速编排。

Docker-Compose 项目由 Python 编写，调用 Docker 服务提供的API来对容器进行管理。因此，只要所操作的平台支持 Docker API，就可以在其上利用Compose 来进行编排管理。

首先检查 版本

```auto
[root@k8s-master ~]#  /usr/local/bin/docker-compose -version
docker-compose version 1.25.1, build a82fef07

```

如果安装好了，就ok了，如果没有安装，则安装docker

1.从github上下载docker-compose二进制文件安装

下载最新版的docker-compose文件

```auto
# curl -L https://github.com/docker/compose/releases/download/1.25.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

> 注明：离线安装包已经提供。上传后，复制到/usr/local/bin/即可

```auto
cp /root/docker-compose  /usr/local/bin/

```

添加可执行权限

```auto
# chmod +x /usr/local/bin/docker-compose
```

测试安装结果

```auto
 

[root@localhost ~]# docker-compose --version 
docker-compose version 1.25.1, build a82fef07


cp /root/docker-compose  /usr/local/bin/
chmod +x /usr/local/bin/docker-compose
 docker-compose --version
```

## 总结：docker改变了什么

+   面向产品：产品交付
+   面向开发：简化环境配置
+   面向测试：多版本测试
+   面向运维：环境一致性
+   面向架构：自动化扩容（微服务）

## 聊聊：docker是怎么工作的?

实际上docker使用了常见的CS架构，也就是client-server模式，docker client负责处理用户输入的各种命令，比如docker build、docker run，真正工作的其实是server，也就是docker demon，值得注意的是，docker client和docker demon可以运行在同一台机器上。

Docker是一个Client-Server结构的系统，Docker守护进程运行在主机上， 然后通过Socket连接从客户端访问，守护进程从客户端接受命令并管理运行在主机上的容器。守护进程和客户端可以运行在同一台机器上。

## 聊聊：docker的工作原理是什么，讲一下

docker是一个Client-Server结构的系统，docker守护进程运行在宿主机上，

守护进程从客户端接受命令并管理运行在主机上的容器，容器是一个运行时环境，这就是我们说的集装箱。

## 聊聊：docker架构

![终于有人把 Docker 讲清楚了](https://imgconvert.csdnimg.cn/aHR0cDovL3AzLnBzdGF0cC5jb20vbGFyZ2UvcGdjLWltYWdlL2ZkOTZiNmRmYWNhNjRkNjk5ZTkzMTRiNzA0NGFhMzNh?x-oss-process=image/format,png)

+   distribution 负责与docker registry交互，上传洗澡镜像以及v2 registry 有关的源数据
+   registry负责docker registry有关的身份认证、镜像查找、镜像验证以及管理registry mirror等交互操作
+   image 负责与镜像源数据有关的存储、查找，镜像层的索引、查找以及镜像tar包有关的导入、导出操作
+   reference负责存储本地所有镜像的repository和tag名，并维护与镜像id之间的映射关系
+   layer模块负责与镜像层和容器层源数据有关的增删改查，并负责将镜像层的增删改查映射到实际存储镜像层文件的graphdriver模块
+   graghdriver是所有与容器镜像相关操作的执行者

## 聊聊：docker的组成包含哪几大部分

一个完整的docker有以下几个部分组成：  
1、docker client，客户端，为用户提供一系列可执行命令，用户用这些命令实现跟 docker daemon 交互；  
2、docker daemon，守护进程，一般在宿主主机后台运行，等待接收来自客户端的请求消息；  
3、docker image，镜像，镜像run之后就生成为docker容器；  
4、docker container，容器，一个系统级别的服务，拥有自己的ip和系统目录结构；运行容器前需要本地存在对应的镜像，如果本地不存在该镜像则就去镜像仓库下载。

docker 使用客户端-服务器 (C/S) 架构模式，使用远程api来管理和创建docker容器。docker 容器通过 docker 镜像来创建。容器与镜像的关系类似于面向对象编程中的对象与类。

## 聊聊：docker技术的三大核心概念是什么？

**镜像：**

镜像是一种轻量级、可执行的独立软件包，它包含运行某个软件所需的所有内容，我们把应用程序和配置依赖打包好形成一个可交付的运行环境(包括代码、运行时需要的库、环境变量和配置文件等)，这个打包好的运行环境就是image镜像文件。  
**容器：**

容器是基于镜像创建的，是镜像运行起来之后的一个实例，容器才是真正运行业务程序的地方。如果把镜像比作程序里面的类，那么容器就是对象。

**镜像仓库：**

存放镜像的地方，研发工程师打包好镜像之后需要把镜像上传到镜像仓库中去，然后就可以运行有仓库权限的人拉取镜像来运行容器了。

### **聊聊：基本的Docker使用流程**

1.  一切都从Dockerfile开始。Dockerfile是镜像的源代码。
2.  创建Dockerfile后，您可以构建它以创建容器的镜像。镜像只是“源代码”的“编译版本”，即Dockerfile。
3.  获得容器的镜像后，应使用注册表重新分发容器。注册表就像一个git存储库 - 你可以推送和拉取镜像。
4.  接下来，您可以使用该镜像来运行容器。在许多方面，正在运行的容器与虚拟机（但没有管理程序）非常相似。

### 聊聊：Docker 安全么？

Docker 利用了 Linux 内核中很多安全特性来保证不同容器之间的隔离，并且通  
过签名机制来对镜像进行验证。大量生产环境的部署证明，Docker 虽然隔离性无法与  
虚拟机相比，但仍然具有极高的安全性。

### 聊聊：Docker 与 虚拟机 有何不同？

Docker 不是虚拟化方法。它依赖于实际实现基于容器的虚拟化或操作系统级虚拟化的其他工具。为此，Docker 最初使用 LXC 驱动程序，然后移动到libcontainer 现在重命名为 runc。Docker 主要专注于在应用程序容器内自动部署应用程序。应用程序容器旨在打包和运行单个服务，而系统容器则设计为运行多个进程，如虚拟机。因此，Docker 被视为容器化系统上的容器管理或应用程序部署工具。

+   容器不需要引导操作系统内核，因此可以在不到一秒的时间内创建容器。此功能使基于容器的虚拟化比其他虚拟化方法更加独特和可取。
+   由于基于容器的虚拟化为主机增加了很少或没有开销，因此基于容器的虚拟化具有接近本机的性能。
+   对于基于容器的虚拟化，与其他虚拟化不同，不需要其他软件。
+   主机上的所有容器共享主机的调度程序，从而节省了额外资源的需求。
+   与虚拟机映像相比，容器状态（Docker 或 LXC 映像）的大小很小，因此容器映像很容易分发。
+   容器中的资源管理是通过 cgroup 实现的。Cgroups 不允许容器消耗比分配给它们更多的资源。虽然主机的所有资源都在虚拟机中可见，但无法使用。这可以通过在容器和主机上同时运行 top 或 htop 来实现。所有环境的输出看起来都很相似。

![img](https://img-blog.csdnimg.cn/20200430191254272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1aHVhZ3Vfd3VodWFndW8=,size_16,color_FFFFFF,t_70)

| 特性    | Docker       | 虚拟机    |
| ----- | ------------ | ------ |
| 启动速度  | 秒级           | 分钟级    |
| 交付/部署 | 开发、测试、生产环境一致 | 无成熟体系  |
| 性能    | 近似物理机        | 性能损耗大  |
| 体量    | 极小（MB）       | 较大（GB） |
| 迁移/扩展 | 跨平台，可复制      | 较为复杂   |

## 聊聊：docker与传统虚拟机的区别什么？

1、传统虚拟机是需要安装整个操作系统的，然后再在上面安装业务应用，启动应用，通常需要几分钟去启动应用，而docker是直接使用镜像来运行业务容器的，其容器启动属于秒级别；  
2、Docker需要的资源更少，Docker在操作系统级别进行虚拟化，Docker容器和内核交互，几乎没有性能损耗，而虚拟机运行着整个操作系统，占用物理机的资源就比较多;  
3、Docker更轻量，Docker的架构可以共用一个内核与共享应用程序库，所占内存极小;同样的硬件环境，Docker运行的镜像数远多于虚拟机数量，对系统的利用率非常高;  
4、与虚拟机相比，Docker隔离性更弱，Docker属于进程之间的隔离，虚拟机可实现系统级别隔离;  
5、Docker的安全性也更弱，Docker的租户root和宿主机root相同，一旦容器内的用户从普通用户权限提升为root权限，它就直接具备了宿主机的root权限，进而可进行无限制的操作。虚拟机租户root权限和宿主机的root虚拟机权限是分离的，并且虚拟机利用如Intel的VT-d和VT-x的ring-1硬件隔离技术，这种技术可以防止虚拟机突破和彼此交互，而容器至今还没有任何形式的硬件隔离;  
6、Docker的集中化管理工具还不算成熟，各种虚拟化技术都有成熟的管理工具，比如：VMware vCenter提供完备的虚拟机管理能力;  
7、Docker对业务的高可用支持是通过快速重新部署实现的，虚拟化具备负载均衡，高可用、容错、迁移和数据保护等经过生产实践检验的成熟保障机制，Vmware可承诺虚拟机99.999%高可用，保证业务连续性;  
8、虚拟化创建是分钟级别的，Docker容器创建是秒级别的，Docker的快速迭代性，决定了无论是开发、测试、部署都可以节省大量时间;  
9、虚拟机可以通过镜像实现环境交付的一致性，但镜像分发无法体系化，Docker在Dockerfile中记录了容器构建过程，可在集群中实现快速分发和快速部署。

### 聊聊：Docker与LXC ( Linux Container)有何不同？

LXC利用Linux上相关技术实现了容器支持； Docker早期版本中使用了LXC技术，后期演化为新的 libcontainer, 在如下的几个方面进行了改进：

+   移植性： 通过抽象容器配置， 容器可以实现从一个平台移植到另一个平台；
+   镜像系统： 基于AUFS的镜像系统为容器的分发带来了很多的便利， 同时共同的镜像层只需要存储一份，实现高效率的存储；
+   版本管理： 类似于Git的版本管理理念， 用户可以更方便地创建、 管理镜像文件；
+   仓库系统： 仓库系统大大降低了镜像的分发和管理的成本；
+   周边工具： 各种现有工具（配置管理、 云平台）对Docker的支持， 以及基于Docker 的PaaS、CI等系统， 让Docker的应用更加方便和多样化。

### 聊聊：什么是 Docker 镜像？

Docker 镜像是 Docker 容器的源代码，Docker 镜像用于创建容器。使用build 命令创建镜像。

### 聊聊：什么是 Docker 容器？

Docker 容器包括应用程序及其所有依赖项，作为操作系统的独立进程运行。

### 聊聊：Docker 容器有几种状态？

四种状态：运行、已暂停、重新启动、已退出。

### 聊聊：Dockerfile 中最常见的指令是什么？

+   FROM：指定基础镜像
+   LABEL：功能是为镜像指定标签
+   RUN：运行指定的命令
+   CMD：容器启动时要运行的命令

### 聊聊：Dockerfile 中的命令 COPY 和 ADD 命令有什么区别？

COPY 与 ADD 的区别 COPY 的 SRC 只能是本地文件，其他用法一致。 8. 解释一下 Dockerfile 的 ONBUILD 指令？ 当镜像用作另一个镜像构建的基础时，ONBUILD 指令向镜像添加将在稍后执行的触发指令。如果要构建将用作构建其他镜像的基础的镜像（例如，可以使用特定于用户的配置自定义的应用程序构建环境或守护程序），这将非常有用。

### 聊聊：docker常用命令？

+   docker pull 拉取或者更新指定镜像
+   docker push 将镜像推送至远程仓库
+   docker rm 删除容器
+   docker rmi 删除镜像
+   docker images 列出所有镜像
+   docker ps 列出所有容器

**1、如何列出可运行的容器?**  
docker ps

**2、启动nginx容器（随机端口映射），并挂载本地文件目录到容器html的命令是？**  
docker run -d -P --name nginx2 -v /home/nginx:/usr/share/nginx/html nginx

**3、进入容器的方法有哪些？**  
1、使用 docker attach 命令  
2、使用 exec 命令，例如docker exec -i -t 784fd3b294d7 /bin/bash

**4、容器与主机之间的数据拷贝命令是？**  
docker cp 命令用于容器与主机之间的数据拷贝  
主机到容器：  
docker cp /www 96f7f14e99ab:/www/  
容器到主机：  
docker cp 96f7f14e99ab:/www /tmp/

**5、当启动容器的时候提示：exec format error？如何解决问题**  
检查启动命令是否有可执行权限，进入容器手工运行脚本进行排查。

**6、本地的镜像文件都存放在哪里？**  
与 Docker 相关的本地资源都存放在/var/lib/docker/目录下，其中 container 目录存放容器信息，graph 目录存放镜像信息，aufs 目录下存放具体的内容文件。

**7、如何退出一个镜像的 bash，而不终止它？**  
按 Ctrl-p Ctrl-q。

**8、退出容器时候自动删除?**  
使用 –rm 选项，例如 sudo docker run –rm -it ubuntu

**9、如何批量清理临时镜像文件？**  
可以使用 sudo docker rmi $(sudo docker images -q -f danging=true)命令

**10、如何查看镜像支持的环境变量？**  
使用 sudo docker run IMAGE env

**11、本地的镜像文件都存放在哪里**  
于 Docker 相关的本地资源存放在/var/lib/docker/目录下，其中 container 目录  
存放容器信息，graph 目录存放镜像信息，aufs 目录下存放具体的镜像底层文件。

**12、容器退出后，通过 docker ps 命令查看不到，数据会丢失么？**  
容器退出后会处于终止（exited）状态，此时可以通过 docker ps -a 查看，其中数据不会丢失，还可以通过 docker start 来启动，只有删除容器才会清除数据。

**13、如何停止所有正在运行的容器？**  
使用 docker kill $(sudo docker ps -q)

**14、如何清理批量后台停止的容器？**  
答：使用 docker rm $（sudo docker ps -a -q）

**15、如何临时退出一个正在交互的容器的终端，而不终止它？**  
按 Ctrl+p，后按 Ctrl+q，如果按 Ctrl+c 会使容器内的应用进程终止，进而会使容器终止。

## 说说: Dockerfile的基本指令有哪些？

FROM 指定基础镜像（必须为第一个指令，因为需要指定使用哪个基础镜像来构建镜像）；  
MAINTAINER 设置镜像作者相关信息，如作者名字，日期，邮件，联系方式等；  
COPY 复制文件到镜像；  
ADD 复制文件到镜像（ADD与COPY的区别在于，ADD会自动解压tar、zip、tgz、xz等归档文件，而COPY不会，同时ADD指令还可以接一个url下载文件地址，一般建议使用COPY复制文件即可，文件在宿主机上是什么样子复制到镜像里面就是什么样子这样比较好）；  
ENV 设置环境变量；  
EXPOSE 暴露容器进程的端口，仅仅是提示别人容器使用的哪个端口，没有过多作用；  
VOLUME 数据卷持久化，挂载一个目录；  
WORKDIR 设置工作目录，如果目录不在，则会自动创建目录；  
RUN 在容器中运行命令，RUN指令会创建新的镜像层，RUN指令经常被用于安装软件包；  
CMD 指定容器启动时默认运行哪些命令，如果有多个CMD，则只有最后一个生效，另外，CMD指令可以被docker run之后的参数替换；  
ENTRYOINT 指定容器启动时运行哪些命令，如果有多个ENTRYOINT，则只有最后一个生效，另外，如果Dockerfile中同时存在CMD和ENTRYOINT，那么CMD或docker run之后的参数将被当做参数传递给ENTRYOINT；

## 说说: 如何进入容器？使用哪个命令

进入容器有两种方法：docker attach、docker exec；  
docker attach命令是attach到容器启动命令的终端，docker exec 是另外在容器里面启动一个TTY终端。

```bash
docker run -d centos /bin/bash -c "while true;do sleep 2;echo I_am_a_container;done"
3274412d88ca4f1d1292f6d28d46f39c14c733da5a4085c11c6a854d30d1cde0
docker attach 3274412d88ca4f						#attach进入容器
Ctrl + c  退出，Ctrl + c会直接关闭容器终端，这样容器没有进程一直在前台运行就会死掉了
Ctrl + pq 退出（不会关闭容器终端停止容器，仅退出）

docker exec -it 3274412d88ca /bin/bash				#exec进入容器	
[root@3274412d88ca /]# ps -ef						#进入到容器了开启了一个bash进程
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 05:31 ?        00:00:01 /bin/bash -c while true;do sleep 2;echo I_am_a_container;done
root        306      0  1 05:41 pts/0    00:00:00 /bin/bash
root        322      1  0 05:41 ?        00:00:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 2
root        323    306  0 05:41 pts/0    00:00:00 ps -ef
[root@3274412d88ca /]#exit							#退出容器，仅退出我们自己的bash窗口

```

小结：

attach是直接进入容器启动命令的终端，不会启动新的进程；

exec则是在容器里面打开新的终端，会启动新的进程；一般建议已经exec进入容器。

### 聊聊：什么是 Docker Swarm？

Docker Swarm 是 Docker 的本机群集。它将 Docker 主机池转变为单个虚拟Docker 主机。Docker Swarm 提供标准的 Docker API，任何已经与 Docker守护进程通信的工具都可以使用 Swarm 透明地扩展到多个主机。

### 聊聊：容器内部机制？

每个容器都在自己的命名空间中运行，但使用与所有其他容器完全相同的内核。发生隔离是因为内核知道分配给进程的命名空间，并且在API调用期间确保进程只能访问其自己的命名空间中的资源。

### 聊聊：什么是Docker Hub？

Docker hub是一个基于云的注册表服务，允许您链接到代码存储库，构建镜像并测试它们，存储手动推送的镜像以及指向Docker云的链接，以便您可以将镜像部署到主机。它为整个开发流程中的容器镜像发现，分发和变更管理，用户和团队协作以及工作流自动化提供了集中资源。

### **聊聊：镜像与** UnionFS

Linux 的命名空间和控制组分别解决了不同资源隔离的问题，前者解决了进程、网络以及文件系统的隔离，后者实现了 CPU、内存等资源的隔离，但是在 Docker 中还有另一个非常重要的问题需要解决 - 也就是镜像。

Docker 镜像其实本质就是一个压缩包，我们可以使用命令将一个 Docker 镜像中的文件导出，你可以看到这个镜像中的目录结构与 Linux 操作系统的根目录中的内容并没有太多的区别，可以说 Docker 镜像就是一个文件。

### **存储驱动**

Docker 使用了一系列不同的存储驱动管理镜像内的文件系统并运行容器，这些存储驱动与

Docker 卷（volume）有些不同，存储引擎管理着能够在多个容器之间共享的存储。

### 聊聊：docker容器之间怎么隔离?

Linux中的PID、IPC、网络等资源是全局的，而NameSpace机制是一种资源隔离方案，在该机制下这些资源就不再是全局的了，而是属于某个特定的NameSpace，各个NameSpace下的资源互不干扰。

虽然有了NameSpace技术可以实现资源隔离，但进程还是可以不受控的访问系统资源，比如CPU、内存、磁盘、网络等，为了控制容器中进程对资源的访问，Docker采用control groups技术(也就是cgroup)，有了cgroup就可以控制容器中进程对系统资源的消耗了，比如你可以限制某个容器使用内存的上限、可以在哪些CPU上运行等等。

有了这两项技术，容器看起来就真的像是独立的操作系统了。

### 聊聊：仓库( Repository)、 注册服务器( Registry)、 注册索引( Index)有何关系？

仓库是存放一组关联镜像的集合，比如同一个应用的不同版本的镜像。注册服务器是存放实际的镜像文件的地方。注册索引则负责维护用户的账号、权限、搜索、标签等的管理。因此，注册服务器利用注册索引来实现认证等管理。

### 聊聊：如何在生产中监控 Docker？

Docker 提供 docker stats 和 docker 事件等工具来监控生产中的 Docker。

我们可以使用这些命令获取重要统计数据的报告。

Docker 统计数据：当我们使用容器 ID 调用 docker stats 时，我们获得容器的CPU，内存使用情况等。它类似于 Linux 中的 top 命令。

Docker 事件：Docker 事件是一个命令，用于查看 Docker 守护程序中正在进行的活动流。 一些常见的 Docker 事件：attach，commit，die，detach，rename，destroy 等。我们还可以使用各种选项来限制或过滤我们感兴趣的事件。

### **聊聊：**如何在多个环境中使用**Docker？**

可以进行以下更改：

+   删除应用程序代码的任何卷绑定，以便代码保留在容器内，不能从外部更改
+   绑定到主机上的不同端口
+   以不同方式设置环境变量（例如，减少日志记录的详细程度，或启用电子邮件发送）
+   指定重启策略（例如，重启：始终）以避免停机
+   添加额外服务（例如，日志聚合器）

因此，您可能希望定义一个额外的Compose文件，例如production.yml，它指定适合生产的配置。此配置文件只需要包含您要从原始Compose文件中进行的更改。

### 聊聊：Docker能在非Linux平台（比如 `macOS`或 `Windows`)上运行么？

可以。

macOS目前需要使用 docker for mac等软件创建一个轻量级的Linux虚拟机层。 由于成熟度不高，暂时不推荐在Windows环境中使用Docker。

###说说: centos镜像几个G，但是docker centos镜像才几百兆，这是为什么？

一个完整的Linux操作系统包含Linux内核和rootfs根文件系统，即我们熟悉的/dev、/proc/、/bin等目录。

我们平时看到的centOS除了rootfs，还会选装很多软件，服务，图形桌面等，所以centOS镜像有好几个G也不足为奇。  
而对于容器镜像而言，所有容器都是共享宿主机的Linux 内核的，

而对于docker镜像而言，docker镜像只需要提供一个很小的rootfs根文件系统即可，只需要包含即我们熟悉的/dev、/proc/、/bin等目录，这是最基本的命令，工具，程序库即可，

所以，docker镜像才会这么小。

### 说说: 镜像的分层结构以及为什么要使用镜像的分层结构？

一个新的镜像其实是从 base 镜像一层一层叠加生成的。

每安装一个软件，dockerfile中使用RUM命令，就会在现有镜像的基础上增加一层，这样一层一层的叠加最后构成整个镜像。

所以我们docker pull拉取一个镜像的时候会看到docker是一层层拉去的。

分层机构最大的一个好处就是 ： 共享资源。

比如：有多个镜像都从相同的 base 镜像构建而来，那么 Docker Host 只需在磁盘上保存一份 base 镜像；

同时内存中也只需加载一份 base 镜像，就可以为所有容器服务了。而且镜像的每一层都可以被共享。

### 说说: 容器的copy-on-write特性，修改容器里面的内容会修改镜像吗？

我们知道，镜像是分层的，镜像的每一层都可以被共享，同时，镜像是只读的。

当一个容器启动时，一个新的可写层被加载到镜像的顶部，这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”。


实际上，docker hub中99%的镜像都是通过在base镜像中安装和配置需要的软件构建出来的

新的镜像是从base镜像一层一层叠加生成的，每安装一个软件，就在现有的基础增加一层  

为什么docker镜像要采用这种分层结构呢？

最大的一个好处是：共享资源

比如:有多个镜像都从相同的base镜像构建而来，那么docker host只需在磁盘上保存一份base镜像: 同时内存中也只需加载一份base镜像，就可以为所有容器服务了，而其镜像的每一层都可以被共享

问题是: 如果多个容器共享一份基础镜像，当某个容器修改了基础镜像的内容，比如/etc下的文件，这时其他容器的/etc是否也会被修改？？？ 答案是不会

修改会被限制在单个容器内, 这就是 容器copy-on-write特性

所有对容器的改动 - 无论添加、删除、还是修改文件，都只会发生在容器层中，

因为只有容器层是可写的，容器层下面的所有镜像层都是只读的。

镜像层数量可能会很多，所有镜像层会联合在一起组成一个统一的文件系统。

如果不同层中有一个相同路径的文件，比如 /a，上层的 /a 会覆盖下层的 /a，也就是说用户只能访问到上层中的文件 /a。

在容器层中，用户看到的是一个叠加之后的文件系统。

添加文件时：在容器中创建文件时，新文件被添加到容器层中。  
读取文件：在容器中读取某个文件时，Docker 会从上往下依次在各镜像层中查找此文件。一旦找到，立即将其复制到容器层，然后打开并读入内存。  
修改文件：在容器中修改已存在的文件时，Docker 会从上往下依次在各镜像层中查找此文件。一旦找到，立即将其复制到容器层，然后修改之。  
删除文件：在容器中删除文件时，Docker 也是从上往下依次在镜像层中查找此文件。找到后，会在容器层中记录下此删除操作。

只有当需要修改时才复制一份数据，这种特性被称作 Copy-on-Write。可见，容器层保存的是镜像变化的部分，不会对镜像本身进行任何修改。

### 说说: Dockerfile的整个构建镜像过程

1、首先，创建一个目录用于存放应用程序以及构建过程中使用到的各个文件等；

2、然后，在这个目录下创建一个Dockerfile文件，一般建议Dockerfile的文件名就是Dockerfile；

3、编写Dockerfile文件，编写指令，如，使用FORM指令指定基础镜像，COPY指令复制文件，RUN指令指定要运行的命令，ENV设置环境变量，EXPOSE指定容器要暴露的端口，WORKDIR设置当前工作目录，CMD容器启动时运行命令，等等指令构建镜像；

4、Dockerfile编写完成就可以构建镜像了，使用`docker build -t 镜像名:tag .` 命令来构建镜像，最后一个点是表示当前目录，docker会默认寻找当前目录下的Dockerfile文件来构建镜像，如果不使用默认，可以使用-f参数来指定dockerfile文件，如：`docker build -t 镜像名:tag -f /xx/xxx/Dockerfile` ；

5、使用docker build命令构建之后，docker就会将当前目录下所有的文件发送给docker daemon，顺序执行Dockerfile文件里的指令，在这过程中会生成临时容器，在临时容器里面安装RUN指定的命令，安装成功后，docker底层会使用类似于docker commit命令来将容器保存为镜像，然后删除临时容器，以此类推，一层层的构建镜像，运行临时容器安装软件，直到最后的镜像构建成功。

### 说说: Dockerfile构建镜像出现异常，如何排查？

首先，Dockerfile是一层一层的构建镜像，期间会产生一个或多个临时容器，构建过程中其实就是在临时容器里面安装应用，如果因为临时容器安装应用出现异常导致镜像构建失败，这时容器虽然被清理掉了，但是期间构建的中间镜像还在，那么我们可以根据异常时上一层已经构建好的临时镜像，将临时镜像运行为容器，然后在容器里面运行安装命令来定位具体的异常。
