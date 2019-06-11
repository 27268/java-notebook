# JVM

java virtual machine——实现平台无关性的重要特点。不同平台的解释器不同，虚拟机都是相同的。当一个程序开始运行，JVM开始实例化，多个程序运行就会有多个虚拟机实例，程序关闭或退出时，JVM实例也随之消亡，多个虚拟机实例之间数据不共享。

## 1. java程序执行

1. 编译（ .java -&gt; .class ）：javac
2. 装载 .class 文件：ClassLoader
3. 执行 .clsdd 文件

* 解释执行
* 编译执行
  * client compiler
  * server compiler

Hotspot JVM 是 sun JDK 和 open JDK中所带的虚拟机。Hotspot JVM中的java 线程与原生操作系统的线程有直接的映射关系；

1. 线程的本地存储、缓冲区、同步对象、栈、程序计数器都准备好之后，会创建一个操作系统原生线程；
2. 原生线程初始化之后，调用java线程的 run\(\) 方法；
3. 由操作系统负责调度所有线程；
4. java线程结束之后，释放原生线程和java线程的资源。

Hotspot JVM 后台运行的系统线程有：

* 虚拟机线程
* 周期性线程任务
* GC线程
* 编译器线程
* 信号分发线程

## 2. 内存模型

{% page-ref page="memory-model.md" %}



### 2.1 内存空间

* 方法区 / 元空间
* 堆
* 方法栈
* 本地方法栈
* pc寄存器

### 2.2 内存分配

#### 堆上分配

#### TLAB分配

#### 栈上分配

### 2.3 内存回收

#### 算法

* copy
* mark-sweep
* mark-compact

#### sun JDK

* 分代回收
* GC参数
* G1

### 2.4 内存状况分析



## 3. JVM线程

### 3.1 线程资源同步

### 3.2 线程交互机制

### 3.3 线程状态分析方法

