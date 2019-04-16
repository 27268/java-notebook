---
description: 图灵
---

# Java技术大纲

## 互联网工程专题

### git

* 搭建git客户端与服务器
  * 基于Linux搭建git服务器
  * 基于ssh开放git服务器
  * git客户端的基本使用
* git的核心命令
  * 本地仓库
    * 新建与远程克隆
    * add与commit
  * 远程仓库
    * 本地仓库、远程仓库、中心仓库
    * 远程仓库添加及状态查看
  * 分支管理与标签
    * 分支创建、回滚、合并，冲突解决，分之状态与commit记录
    * label使用
* git企业应用
  * git web服务器搭建与使用
    * gogs安装、自动备份与恢复、迁移、核心操作
    * gogs bugs
  * 企业版本迭代分支管理经验

### Maven

* Maven体系结构
  * Maven架构思路
  * Maven内部运作原理
    * Maven生命周期与插件体系
* Maven核心命令
  * Clean，compile，test，package，install，deploy
* maven的pom配置体系
  * 模块配置，属性配置，依赖配置，构建配置，插件配置
* 搭建Nexus私服

### Jenkins

* 可持续集成的概念：持续集成、持续交互、持续部署
* Jenkins详解
* Jenkins实践
  * 构建环境配置
  * 配置自动部署
  * 远程仓库推送
  * 自动触发构建
* Jenkins插件体系：常见插件的安装与使用、插件开发

### Linux

* Linux原理、启动、目录介绍
* Linux运维常用命令
* Linux用户与权限介绍
* shell脚本

Linux：系统内核、shell、文件系统、实用工具。系统内核对外提供系统调用借口，shell、文件系统、实用工具通过访问系统调用，实现自身功能。

系统内核的功能：

* 进程调度：控制进程对CPU资源的访问，多任务系统中存在多个可以被调度的任务。等待其他资源\(cpu之外的资源\)的进程将处于睡眠状态，等资源就绪后，进程被唤醒，等待再次被调度。 Linux的内存调度方法：优先级
* 内存管理：linux支持以虚拟内存的方式进行内存管理。 虚拟内存：将磁盘作为内存的扩展，程序被调入内存后，若程序、堆栈、数据的总容量超过内存的实际大小，内核会将当前使用的程序块保存在内存中，其他内容保存在磁盘中，当执行到磁盘中的内容时，内核会负责在磁盘和内存之间交换数据，这里就用到Linux的交换区。
* 虚拟文件系统VFS，向用户提供统一的访问接口。 用户程序 -&gt; VFS -&gt; {fat, ext2, ext3, ISO-9660, ... } -&gt; 设备驱动程序 -&gt; {磁盘，光盘，闪盘}
* 进程间通信机制
  * 本机进程间通信的消息队列、共享内存、信号量
  * 网络环境进程通信：套接口socket
  * POSIX通信机制

```text
$ uname -r 
4.15.0-29deepin-generic //查看系统内核版本
$ uname -a //查看系统发行版本。发行版本：软件厂商
Linux liuyi-PC 4.15.0-29deepin-generic #31 SMP Fri Jul 27 07:12:08 UTC 2018 x86_64 GNU/Linux

$ sudo fdisk -l 
Disk /dev/sda: 931.5 GiB, 1000204886016 bytes, 1953525168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x81fcf99d

Device     Boot      Start        End    Sectors   Size Id Type
/dev/sda1  *          2048 1936855039 1936852992 923.6G 83 Linux
/dev/sda2       1936857086 1953523711   16666626     8G  5 Extended
/dev/sda5       1936857088 1953523711   16666624     8G 82 Linux swap / Solaris

```

进程调度策略：分时调度sched\_other、先到先服务的实时调度sched\_fifo、时间片轮转的实时调度sched\_rr

shell 为用户提供交互操作的接口

## 框架

### Spring

* Spring framework
  * Spring体系结构
  * Spring IOC 容器设计原理
  * IOC bean生命周期
  * Spring context装载过程
  * FactoryBean与BeanFactory
* Spring MVC
  * MVC设计思想与体系结构（dispatchServlet）
  * MVC执行流程
  * requestMapping实现原理
  * MVC组件体系：映射器、执行适配器、视图解析器、异常捕捉器原理
* Spring AOP
  * AOP编程概念
  * 基于AOP实现应用插件机制
  * AOP底层实现
* Spring 5
  * 新特性详解
  * 响应式编程模型
  * SpringWebFlux

### ORM框架MyBatis

* myBatis体系结构
  * 与传统JDBC的对比，与hibernate的对比
  * myBatis全局参数
  * 逆向工程
  * 详解configuration，properties，setting，typeAlises，mapper
  * xml，annotations，criteria
* 与Spring的集成
* myBatis源码分析：Configuration、Mapper、SqlSession、Executor
* myBatis中用到的设计模式：工厂模式、构建模式、单例模式、责任链模式、代理模式、模板模式、装饰模式
* myBatis运行机制
  * 内部运行机制与初始化过程
  * 二级缓存应用

## 并发编程专题

### executor线程池

```java
public interface Future{}
public interface Executor{}
```

### locks

### tools限制

* CountDownLatch
* Semaphore

### atomic原子性

* atomic类，ThreadLocal，ABA，JMM，cas

### collections

* ConcurrentQueue
* Map
  * ConcurrentHashMap
  * HashMap, HashTable
* Concurrent List, Set

### ForkJoin框架

* 框架介绍
* 案例
* 原理

### 内存模型

* 重排序、可见性、顺序一致性、happens-before规则
* synchronized volatile ThreadLocal

## 性能调优专题

### JVM性能调优

* jvm内存模型
  * 堆空间，方法区， 线程计数器，线程栈，本地方法栈
  * **直接内存**
* 内存管理
  * 垃圾回收机制
    * 垃圾收集器：G1, Serial, ParNew, ParallelScavenge, Serial old, CMS\(concurrent mark sweep\)
    * 垃圾收集算法：标记-清除（Mark-sweep），复制算法、标记-整理、分代收集
  * 调优工具
    * jdk命令：jps, jstat, jinfo, jmap, jhat, jstack
    * jconsole
    * jvisualvm
* 类加载机制：类加载器和双亲委派机制
* JVM调优：GC日志分析、JVM参数调优分析

### MySQL性能调优

* 索引数据结构：B+树、红黑树、二叉树
* MySQL执行计划与索引优化：explain工具、索引优化
* MySQL锁机制和事务隔离级别
  * 锁机制
    * 性能（乐观锁、悲观锁）
    * 操作（读锁、写锁）
    * 粒度（表锁、行锁）
    * 死锁及优化解决
  * 事务隔离级别
    * 读未提交
    * 读已提交
    * 可重复读（MVCC机制）
    * 串行化
  * 复杂SQL语句优化

### Nginx调优

* Nginx整体架构：核心模块、标准Http模块、可选http模块、第三方模块、Nginx事件驱动模型
* Nginx核心配置：基本配置、虚拟主机配置、upstream、location、静态目录配置
* Nginx负载均衡算法：轮询+权重，IP hash、URL hash，least\_conn、least\_time

### Tomcat调优

* tomcat项目架构
  * tomcat启动流程，http请求解析与处理流程
  * 核心组件：wrapper, context, host, engine, container
  * tomcat 8 & tomcat 7
* 生产环境配置：server.xml文件、tomcat集群与会话复制方案、tomcat虚拟主机配置
* tomcat线程模型
  * tomcat支持的四种线程模型：NIO、BIO、APR、AIO
  * 通过压测演示NIO与BIO的区别
  * tomcat BIO, NIO源码，
  * connector并发参数

## 分布式框架专题

### 初识分布式

* 分布式系统的定义、意义、基础知识
* 大型网站架构模式
  * 分层、分割模式
  * 分布式（缓存、异步模式，系统冗余、扩展模式）、集群模式
* 大型网站架构要素
  * 高并发原子性：无状态、拆分、服务化、消息队列
  * 高可用原子性：降级、限流、备份、监听

### 分布式中间件

* 分布式服务治理（zookeeper、dubbo）
  * 分布式应用系统服务化通讯技术，从集中到分布式的特点：ACID到CAP/base基础
  * 分布式协同框架Zookeeper
    * zookeeper集群部署、服务注册与订阅、zookeeper迁移、扩容、监控
    * znode、watcher、ACL、客户端API、客户端 服务端源码
  * RPC服务框架Dubbo
    * 分布式架构的历史、入手、风险
    * 常规应用：dubbo作用、demo、架构与基本角色、基本应用与配置
    * 企业级应用：分布式项目开发与连调、dubbo控制管理后台、dubbo注册中心
    * RPC协议底层原理与实现：RPC协议基本组成、报文编码与实现、RPC in dubbo
    * 调用模块：容错、负载均衡、异步调用、过滤器，应用场景：泛华调用与引用、隐式传参、令牌验证，dubbo路由功能
* 分布式消息异步解耦（RocketMq、kafka、Rabbitmq）
  * 常用中间件对比：rocketMq、kafka、rabbitmq、activeMq
  * 分布式消息框架RocketMq
    * 集群部署与快速入门、监控与运维
    * RocketMq模块划分与集群原理
    * 普通消息、顺序消息、事务消息、定时消息
    * RockerMq broker, consumer-producer 源码分析
  * kafka：简介、集群搭建与使用、原理分析
* 分布式数据缓存（redis）
  * 关系型数据库瓶颈与优化，非关系型数据库中间件：mongoDB, redis, tair, memcache, neo4j
  * redis使用场景
  * redis基本数据类型、哨兵机制、复制、常用命令
  * redis cluster原理、集群分配算法与动态水平扩容与监控、
  * jedis cluster开发与通信协议
* 分布式数据存储（sharding-sphere）
  * 分布式场景中的数据库瓶颈，为何要读写分离、分库分表
  * 常见分片算法：hash、list、range、tag，常见中间件：Mycat、sharding-jdbc
  * 分布式数据中间件sharding-jdbc
    * sharding-jdbc快速开始、核心概念，特性详解与模块划分，最新技术sharding-sphere
    * sharding-jdbc源码：SQL解析、SQL路由、SQL改写、SQL执行、结果合并
  * Atlas配置与原理，实践与优缺点

### 分布式通信（Netty）

* NIO线程模型、reactor模型，线程源码分析
* 高性能序列化协议protobuf与源码分析
* 粘包、分包现象及解决方案、编解码器源码分析
* netty之http协议开发（弹幕系统），WebSocket协议开发（多人联机网游）

### 分布式搜索引擎

* 技术点：Elasticsearch、logstash、kibana
* ELk集群搭建实战、架构与原理分析

## 项目实战专题

### 电商平台

* 项目介绍、系统划分&技术实现
  * 会员系统：模块配置、会员业务实现、SSO单点登录、数据库分库分表
  * 商品系统：模块配置、商品业务实现、商品详情页静态化与缓存
  * 订单系统：模块配置、订单业务实现、分布式失误 幂等性 重复问题
  * 后台系统：模块配置、系统权限 资源 账号 权限关系技术实现
* 技术解决方案
  * 高并发秒杀系统的技术实现与限流
  * 商品详情页的缓存击穿与解决方案、整体缓存方案
  * 分布式订单号生成
  * 海量数据：不需要扩容的分库分表方案，读写分离技术方案

### 分布式调用链平台

* 分布式调用链简介、平台概要设计，
* 实现技术：Javaassit，javaagent，字节码插桩，
* 埋点（探针）采集
  * 采集点：Dubbo，JDBC Driver，Spring，Tomcat，http，redis
* 基础知识：类加载器，ThreadLocal、ThreadPool应用
* 分布式环境部署与问题排查

## 微服务系列

微服务发展与产生的意义

### Spring Boot

* 快速开始与核心配置、部署方式及热部署
* web开发末班引擎：thymeleaf，freemarker
* spring boot集成myBatis、redis、rabbitMq、多数据源路由、分布式事务处理
* spring boot源码解析

### Spring Cloud

* eureka服务注册与发现 及源码
* ribbon客户端负载均衡 及源码
* fegin声明式服务调用及源码
* hystrix实现服务限流、降级、熔断
* zuul统一网关，服务路由，过滤器使用，zuul统一异常处理，cookie和重定向
* 分布式配置中心Config
* 分布式链路跟踪

### 虚拟容器

* Docker
  * docker镜像、仓库、容器详解、快速开始
  * DockerFile、DockerCompose使用详解及服务编排实现
* Kubernetes
  * 介绍、快速开始、部署生态环境

## 扩展技术专题

### 人工智能

### 区块链

* 区块链整体结构设计与实现
  * 共识机制
* 密码学
  * 对称加密，非对称加密，hash，数字签名
* 钱包设计与实现
  * 钱包结构
  * 钱包转账
  * 钱包余额
* 交易的设计与实现
  * UTXO与余额
* p2p去中心化网络设计与实现
  * p2p网络
  * 节点发现与节点通讯
  * 区块广播、交易广播

### 大数据

* Hadoop
  * Hadoop资源调度框架Yarn
  * 分布式文件系统HDFS
  * 分布式框架MapReduce
* 大数据通用生态圈组件
  * 数据采集器
  * 数据仓库与OLAP
  * NoSQL数据库
  * Zookeeper与分布式一致性算法
  * 中间件
* Spark及生态圈
  * Spark核心
  * SparkSQL
* 基于Spark的数据挖掘算法
  * 协同滤波 实现推荐系统
  * Spark下的聚类与分类算法
  * Spark下的图计算



