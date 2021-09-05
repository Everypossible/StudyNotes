# 1、Docker概述

## 1、虚拟化技术

硬件级虚拟化 ------ 缺点：每个虚拟机都要安装一个操作系统，这样会造成电脑资源的浪费

操作系统级虚拟化 ------- 模拟的是运行在一个操作系统上的多个不同线程，一个容器里有几个进程，每个容器之间是隔离的，该技术称为容器化技术。

![image-20210819141120810](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210819141120810.png)

![image-20210819141208270](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210819141208270.png)

![image-20210819142338271](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210819142338271.png)

在容器化技术领域，Docker是目前最流行的一种实现。Docker 发布于 2013年，Docker 基于 LXC 技术，LXC 是 Linux 上的容器化技术实现。

注：LXC是Linux Container的简写，它是一种内核虚拟化技术，可以提供轻量级的虚拟化，以便隔离进程和资源，它与宿主机使用同一个内核，性能损耗小，这种技术是Linux提供的，但是直到Docker出世，该技术才被发挥出来。

dotCloud 的核心引擎技术能将 Linux 中的应用代码打包，轻松地在服务器之间迁移，这项技术就是Docker的开端。

## 2、Docker是什么

Docker 是一个 开源的 应用容器引擎，它基于 Google 公司推出的 Go 语言实现，项目托管在 GitHub 上维护。

Docker技术让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，打包好的容器可以发布到任何流行的Linux服务器上运行，这样就可以解决开发环境与运维环境不一致的问题了，所以容器技术解决了开发和运维之间的矛盾，让开发专注于开发，运维专注于运维，不要被环境问题所打扰。

使用Docker的显著优势：Docker彻底释放了虚拟化的威力，极大降低了计算机资源供应的成本，Docker重新定义了程序开发测试、交付和部署过程，Docker提出了 **“构建一次，到处运行”** 的理念，让应用的开发、测试、部署和分发都变得前所未有的高效和轻松。

4、Docker是一种轻量级的操作系统虚拟化解决方案，Docker的基础是Linux 容器(LXC)技术，在LXC的基础上 Docker进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker的容器就像操作一个快速轻量级的虚拟机一样简单；Docker自开源后受到广泛的关注，Docker最早是基于Ubuntu开发的，但后续CentOS、Debian、Fedora等主流的Linux 操作系统都支持Docker。

总结：简单地说，Docker是对软件和其依赖环境的标准化打包，应用之间相互隔离，共享一个OS Kernel（解决了资源浪费的问题），可以运行在很多主流操作系统上；
但是也需要澄清一下，Docker本身不是容器，Docker只是管理容器的引擎。



## 3、为什么要使用 Docker

作为一种新兴的虚拟化技术，Docker跟传统的虚拟化方式相比具有众多的优势。
1、启动快：Docker容器的启动可以在秒级实现，这相比传统的虚拟机方式要快得多。
2、占用资源少：Docker对系统资源的利用率很高，一台主机上可以同时运行数干个Docker 容器。
3、容器除了运行其中的应用外，基本不消耗额外的系统资源，使得应用的性能很高。传统虚拟机方式运行10个完全不同的应用可能我们会起10个虚拟机来部署，而Docker只需要启动10个隔离的应用即可。

6、更轻松的迁移和扩展，Docker容器几乎可以在任意的平台上运行，包括物理机、虚拟机、公有云、私有云、个人电脑、服务器等，这种 **兼容性** 可以让用户 轻松地 把一个应用从一个平台直接迁移到另一个平台。





# 2、Docker 环境搭建

## 1、Docker 的安装

Docker CE即社区免费版，可永久免费使用；（我们日常使用）
Docker EE即企业版，功能更全，更强调安全，但需付费使用；

首先，我们知道Docker并不是容器，它是一个管理容器的引擎。
我们课程采用的Linux版本是CentOS 7,学习Docker 也更推荐在 **Linux** 环境下使用；
Docker 支持 CentOS 6 及以后的版本；
CentOs7系统可以直接通过 **yum** 进行安装：
安装前可以查看一下系统是否已经安装了Docker：使用Linux命令yum list installed | grep docker

安装Docker：使用命令：yum install docker -y

安装后使用命令 docker --version (或者 docker -v ) 查看docker版本

卸载docker：使用命令 yum remove docker -y



## 2、Docker 如何启动

安装之后启动 Docker 服务（CentOS 7 环境下）

启动：systemctl start docker 或者 service docker start

停止：systemctl stop docker 或者 service docker stop

重启：systemctl restart docker 或者 service docker restart

检查 docker 进程的运行状态：systemctl status docker 或者 service docker status

查看 docker 进程：ps -ef | grep docker



### 1、Docker 的服务信息

docker info ------ 查看 docker 的系统信息

docker ------ 查看所有的帮助信息

docker command --help ------ 查看某个 command 命令的帮助信息



### 2、Docker 运行机制

![image-20210819152515466](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210819152515466.png)

下载镜像：使用命令 docker pull tomcat（若本地仓库已有tomcat，则改命令会去 更新 tomcat 版本）

运行（启动）镜像：使用命令 docker run tomcat（这是前台运行）若要后台运行 tomcat镜像，则需要先关闭前台tomcat（CTRL + C）再使用 docker run -d tomcat

查看本地已下载的镜像：使用命令 docker images



docker ps ------ 查看 Linux 中目前正在运行的容器

ps -ef | grep tomcat ------ 查看tomcat镜像 是否启动容器成功

docker stop +docker ps查出的某个容器的ID ------关闭某个容器



从客户机访问容器，需要有端口映射，docker 容器默认采用 **桥接模式** 与宿主机通信，需要将宿主机的 端口ip 映射到 容器的ip端口 上。如：若想访问 容器中 的Tomcat 则必须做端口映射 再启动Tomcat ，将 Linux 端口与 容器端口映射 并启动Tomcat，使用命令docker run -d -p 8080:8080 tomcat（前面的 8080 是 Linux的端口，后面的8080是 容器 的端口）



如何进入 Docker 容器

进入容器：docker exec -it cef0d139bfd6 bash（cef0d139bfd6是这个容器的id，bash是shell脚本命令行，i表示交互式的 也就是保持标准输入流打开，t表示虚拟控制台，分配到一个虚拟控制台）

退出容器：exit





# 3、Docker 核心组件

## 1、Docker 的架构

Docker 使用客户端-服务器（ C / S ）架构模式，使用远程 API 来管理和创建 Docker 容器。

Docker容器 通过 Docker镜像来 创建。

镜像与容器的关系 类似于 面向对象编程中的 类与对象 的关系。



## 2、Docker 核心要素

镜像（Image）、容器（Container）、仓库（Repository）

理解了这三个概念，就理解了Docker的整个生命周期。

Docker 的运行离不开以上核心几个组件的支持，Docker的成功也是拜这几个组件所赐。

有人会误以为，Docker就是容器，但Docker不是容器，而是管理容器的 **引擎**。

### 1、镜像

Docker镜像就是一个只读的模板，可以用来创建Docker容器。
Docker提供了一个非常简单的机制来创建镜像或者更新现有的镜像，用户甚至可以直接从其他人那里下载一个已经做好的镜像来直接使用。

镜像的组成结构：镜像是由许多层的文件系统叠加构成的。最下面是一个引导文件系统 **bootfs** ，第二层是一个root 文件系统 **rootfs**，root 文件系统通常是某种**操作系统**，比如centos、Ubuntu，在root文件系统之上又有很多层文件系统，这些文件系统叠加在一起，构成docker中的镜像；

下载镜像：docker pull redis:latest（redis是查询到的镜像名称，lastest是镜像的版本号）

获取一个镜像有两种方式，一种是从官方镜像仓库下载，一种是自己通过 dockerfile 文件构建。

删除镜像：docker rmi redis:lastest 注意是 rmi 不是 rm，rm是删除 容器。





### 2、容器 

容器是从镜像创建的运行实例。它可以被启动、停止、删除。每个容器都是 **相互隔离** 的、保证安全平台。可以把看做一个简易版的Linux环境，包括root用户权限、进程空间、用户空间和网络空间和运行在其中的应用程序。

Docker利用容器来运行应用，镜像是 **只读** 的，容器在启动的时候创建一层 **可写** 层作为 最上层。

#### 1、容器的日常状态

启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态的容器重新启动。
通过镜像启动容器：docker run-drredis
查看运行中的容器：docker ps
查看所有的容器：docker ps -a
停止容器：docker stop 容器id 或容器名称

已经停止的容器可以重新启动，开启容器：docker start 容器id或容器名称

因为Docker的容器实在太轻量级了，很多时候用户都是随时删除和新创建容器。

删除容器：docker rm 容器id或容器名称
删除容器时，容器必须是停止状态，否则会报错；
进入容器：docker exec-it 容器id 或容器名称 bash
还可以使用docker inspect + 1容器id或容器名称查看容器的更多信息；
停用全部运行中的容器：docker stop $(docker ps -q)
删除全部容器：docker rm $(docker ps -aq)
一条命令实现停用并删除容器：
docker stop $(docker ps -q)& docker rm $(docker ps -aq)







### 3、仓库



