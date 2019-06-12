# mybatis

{% embed url="http://www.mybatis.org/spring/zh/getting-started.html" %}

{% embed url="http://www.mybatis.org/mybatis-3/zh/index.html" %}

重要组件

* SqlSessionFactory
* MapperFactoryBean

使用mybatis的主要java接口是SqlSession，通过SqlSession可以执行命令、获取映射器和管理事务。

### 获取SqlSession

1. SqlSessionFactoryBuilder.build\(resource\) resource中指定了配置参数：environments（包括datasource, transaction manager）, mapper，
2. SqlSessionFactory.openSession\(\)
3. SqlSession
4. 执行语句方法
5. 批量立即更新方法
6. 事务控制方法
7. 本地缓存
8. 关闭SqlSession
9. **使用Mapper**

   3.1 使用Mapper：java方法与SQL语句的映射

   1. 定义Mapper接口
   2. 配置Mappers：resource
   3. mapper = sqlSession.getMapper\(UserMapper.class\);
   4. 通过mapper的方法执行sql语句

```java
SqlSession SqlSessionFactory.openSession()
SqlSession SqlSessionFactory.openSession(boolean autoCommit)
SqlSession SqlSessionFactory.openSession(Connection connection)
SqlSession SqlSessionFactory.openSession(TransactionIsolationLevel level)
SqlSession SqlSessionFactory.openSession(ExecutorType execType,TransactionIsolationLevel level)
SqlSession SqlSessionFactory.openSession(ExecutorType execType)
SqlSession SqlSessionFactory.openSession(ExecutorType execType, boolean autoCommit)
SqlSession SqlSessionFactory.openSession(ExecutorType execType, Connection connection)
```

### DataSource的配置

使用postgresql数据源：依赖包 "org.postgresql:postgresql:9.4.1212.jre7"

```markup
<dataSource type="POOLED">
     <property name="driver" value="org.postgresql.Driver"/>
     <property name="url" value="jdbc:postgresql:blogDB"/>
     <property name="username" value="postgres"/>
     <property name="password" value="123456"/>
</dataSource>
```

## mybatis cache

1. 一级缓存：sqlsession级别 - 默认开启 sqlsession.getMapper\(UserMapper.class\)
2. 二级缓存：mapper级别，可以供多个sqlsession使用

### 一级缓存

mybatis一级缓存的两个选项：

* session
* statement

手动配置：

```markup
<!--value选项：session, statement-->
<setting name="localCacheScope" value="SESSION"/>
```

（ref3） 一级缓存仅在session内部共享，开启两个SqlSession， 在sqlSession1中查询数据，使一级缓存生效， 在sqlSession2中更新数据库，sqlSession2更新了id为1的学生的姓名，从凯伦改为了小岑， 但session1之后的查询中，id为1的学生的名字还是凯伦，出现了脏数据。

!!!多个session或者分布式环境，不要使用session级别的缓存。建议使用statement

sqlsession执行过程：

```text
sqlsession.select()
 -> executor.query()
 -> localCache.getObject()： 两种情况
     -> return null： dispatch to database & get object
                      localCache.putObject()
                      return object
     -> return object
```

源码：

```java
/**
 * sqlsession
 *   -》 executor及其实现类 
 *        -》 BaseExecutor.localCache
 *           -》perpetualCache.cache = new HashMap<Object, Object>()                               
 * -》成员变量
 */
```

### 二级缓存

多个sqlsession共享二级缓存。 **同一个namespace下**的所有操作语句，都影响着同一个Cache，即二级缓存被多个SqlSession共享，是一个全局的变量。 开启二级缓存后，会使用CachingExecutor装饰Executor，（装饰器模式） 进入一级缓存的查询流程前，先在CachingExecutor进行二级缓存的查询，

配置：

```markup
<!--开启二级缓存 in mybatis配置文件 ref3 -->
<setting name="cacheEnabled" value="true"/>

<!--配置二级缓存 in mapper配置文件 ref3 -->
<cache name="type" value="PerpetualCache"/>
```

当sqlsession没有调用commit\(\)方法时，二级缓存并没有起到作用。

通常我们会为每个单表创建单独的映射文件，由于MyBatis的二级缓存是基于namespace的， 多表查询语句所在的namspace无法感应到其他namespace中的语句对多表查询中涉及的表进行的修改，引发脏数据问题。

解决二级缓存中 多表查询的一致性问题：Cache-ref，使多个命名空间中共享相同的缓存配置和实例。

（ref1）开启二级缓存的效果如下:

* 映射语句文件中的所有 select 语句的结果将会被缓存。
* 映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存。
* 缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存。
* 缓存不会定时进行刷新（也就是说，没有刷新间隔）。
* 缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用。
* 缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改。

二级缓存实现原理：

```text

```

### 分布式环境中的缓存

mybatis的缓存 保存在内存中，分布式环境中无法共享，存在数据一致性问题。

解决方案：

* mybatis-redis: 配置mapper的缓存类型为

  ```text
  <mapper>
      <cache type="org.mybatis.caches.redis.RedisCache"/>
      <select id="getUserByID" resultType="User">
          select * from USER_info where id = #{id}
      </select>
  </mapper>
  ```

* mybatis-plus支持分布式事务（2019.04.25更新）

## 代理模式的应用？

## reference

[http://www.mybatis.org/mybatis-3/zh/java-api.html](http://www.mybatis.org/mybatis-3/zh/java-api.html)

[http://www.mybatis.org/spring/zh/getting-started.html\#](http://www.mybatis.org/spring/zh/getting-started.html#)

[https://tech.meituan.com/2018/01/19/mybatis-cache.html](https://tech.meituan.com/2018/01/19/mybatis-cache.html)



