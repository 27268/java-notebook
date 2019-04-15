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
* 与Spring的集成
* myBatis源码分析：Configuration、Mapper、SqlSession、Executor
* myBatis中用到的设计模式：工厂模式、构建模式、单例模式、责任链模式、代理模式、模板模式、装饰模式
* myBatis运行机制
  * 初始化过程
  * 二级缓存应用

## 并发编程专题

### executor线程池

```java
public interface Future{}
```

### locks

### tools限制

### atomic

### collections

### ForkJoin框架

* 框架介绍
* 案例
* 原理

### 内存模型

* 重排序、可见性、顺序一致性、happens-before规则
* synchronized volatile ThreadLocal

## 性能调优专题

### JVM性能调优

* jvm内存模型和内存管理
* 类加载机制：类加载器和双亲委派机制
* JVM调优：GC日志分析、JVM参数调优分析

### MySQL性能调优

* 索引数据结构：B+树、红黑树、二叉树
* MySQL执行计划与索引优化：explain工具、索引优化
* MySQL锁机制和事务隔离级别
  * 锁机制
    * 性能（乐观锁、悲观锁）
    * 操作（读锁、写锁）

### Nginx调优

### Tomcat调优

## 分布式框架专题

### 初识分布式

### 分布式中间件

### 分布式通信（Netty）

## 项目实战专题

### 电商平台

### 分布式调用链平台

## 微服务系列

### Spring Boot

### Spring Cloud

### 虚拟容器

* Docker
* Kubernetes

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



