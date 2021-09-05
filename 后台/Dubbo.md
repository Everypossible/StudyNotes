# 1、Dubbo 基础知识

## 1、分布式系统

​		分布式系统是 **若干 独立计算机** 的集合，这些计算机对于用户来说就像是单个相关系统。分布式系统是建立在网络之上的软件系统。

​		随着互联网的发展，网站应用的规模不断扩大，常规的 垂直系统架构 已无法应对，分布式服务架构 以及 流动计算机架构 势在必行，亟需一个 **治理系统** 确保架构有条不紊地演进。



​		分布式服务框架难点和重点就是：如何 RPC 和将业务进行 拆分部署 到不同服务器上。

​		RPC 【Remote Procedure Call】是指 **远程过程调用**，是一种进程间通信方式，他是十种技术的思想，而不是规范。它允许程序调用另一个地址空间(通常是共享网络的另一台机器上)的过程或函数，而不用程序员显式编码这个远程调用的细节。即程序员无论是调用本地的还是远程的函数，本质上编写的调用代码基本相同。

​		RPC两个核心模块：通讯，序列化。

​		RPC框架有很多如：dubbo、gRPC、Thrift、HSF(High Speed Service Framework)





## 2、Dubbo 核心概念

![image-20210820103943356](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210820103943356.png)



设计架构

![image-20210820104100412](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210820104100412.png)



Register(注册中心) 推荐使用 zookeeper

Monitor 可安装可不安装，安装后只是有了一个可视化界面（怎么启动Monitor？去Dubbo的GitHub上下载 Dubbo OPS，然后 mvn 打包下载下来的OPS，然后去OPS文件夹中的application.properties修改端口号，然后启动zookeeper，再去浏览器中输入端口号访问Monitor）



分包原则

![image-20210820115939833](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210820115939833.png)



将服务提供者注册到注册中心（暴露服务）

​		导入Dubbo依赖、导入zookeeper的客户端（curator）依赖

​		配置服务提供者（provider.xml）

让服务消费者去注册中心订阅服务提供者的服务地址



