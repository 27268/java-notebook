# 1. 线程基础

* 程序——静态 
* 进程——动态，程序的一次执行 
* 线程——进程内的多条执行路径 共享进程的资源，只为线程分配CPU

继承Thread创建线程：

* 实现：继承Thread类，重写run\(\)方法。run方法称为线程体。
* 调用方法：创建子类对象，调用其start方法。start方法由CPU调用。 注意不要自己调用run，start会调用。 main方法也是一条线程，同一时刻只能运行一个线程

实现Runnable接口创建线程：

Runnable方式的设计模式：静态代理

* 真实角色 
* 代理角色：持有真实角色的引用，代理角色与真实角色实现了相同的接口。 
* 使用时：创建真实角色 创建代理角色（包括真实角色的引用） 执行任务 包括静态代理与动态代理。

在多线程中： 

* 相同接口：Runnable接口 
* 代理角色：Thread类 
* 真实角色：实现runnable接口的自定义类

静态代理的实现：

1. Programmer实现Runnable接口，重写run方法。
2. 创建真实角色：Programmer pro = new Programmer\(\); 
3. 创建代理角色及真实角色的引用：Thread poaAgent = new Thread\(pro\); 
4. 执行任务：proAgent.start\(\);

优点： 避免单继承的限制 便于资源共享：?

Thread.currentThread\(\).getName\(\);

线程状态: 

* 新生 
* 就绪 
* 阻塞 
* 运行 
* 结束

结束进程 

* 自然终止：线程体执行结束 
* 外部干涉： 类中定义线程体使用的标识，线程体使用上述标识，类提供改变标识的方法，外部依据标识操作线程状态。
* 停止进程：thread.stop\(\);//尽量不要用

线程调度 

thread.join\(\)方法：合并线程，等thread终止后本线程\(调用该方法的线程\)再执行。

Thread.yield\(\)方法：暂停自己，谁调用谁被暂停

## synchronized关键字

 对资源加锁 用于同步方法、同步语句块

 `public synchronized void test(){}`

`public void test(){  
    synchronized(引用类型/this/类.class){ //需要同步的语句块 } }`

线程安全的难点：确定要加锁的范围。

### synchronized用于单例设计模式

单例设计模式：保证一个类只有一个对象。 

实现方法： 懒汉式 

1. 构造器私有化 
2. 声明一个私有的静态变量（本类对象） 
3. 创建一个对外的静态方法访问该变量，若变量没有对象/为空，创建一个对象。

在实现时，需要用synchronized同步3中的操作 

`synchronized(Single.class){  
//不存在时，创建对象 注意效率问题：已经有对象了，就不要在同步了，直接返回对象即可   } //适用于不是频繁getInstance的对象，因为同步块效率较低`

饿汉式： 

1. 构造器私有化 
2. 声明私有的静态属性，同时创建该对象//加载时间长 
3. 对外提供访问该对象的静态方法

静态内部类

`class A{  
   private static class B{  
       private static A instance = new A();  
   }  
   private A(){}  
   public static A getInstance(){ return B.instance;   
}`

 类在使用时加载，上述使用方式可以延迟加载时间。

java中的单例设计模式：Runtime类

### 死锁

同步方法过多，容易造成死锁

解决方法：生产者消费者模式

wait\(\)与notify\(\)方法用于唤醒线程，只用于线程同步。

Timer类schedule\(timertask,time,period\)方法在指定的时间调用指定任务 其中，TimerTask\(\){run\(\){//任务体}}

QUARTZ框架

### 总结

1、创建线程：三种方法 

2、线程状态：重点关注三个状态，终止/阻塞（join/yield/sleep）线程的方法 

3、线程信息：Thread.currentThread 

4、同步：synchronized针对同一资源 

5、生产者消费者模式 

6、任务调度Timer

后续目标：juc/quartz
