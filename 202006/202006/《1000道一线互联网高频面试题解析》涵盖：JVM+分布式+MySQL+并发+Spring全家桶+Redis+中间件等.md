# 《1000道一线互联网高频面试题解析》涵盖：JVM+分布式+MySQL+并发+Spring全家桶+Redis+中间件等

[![img](https://upload.jianshu.io/users/upload_avatars/13638982/22c4c181-49bf-48e7-bbcf-608d5cad9541.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96)](https://www.jianshu.com/u/4a35811f38e1)

[慕容千语](https://www.jianshu.com/u/4a35811f38e1)[![  ](https://upload.jianshu.io/user_badge/ec7b4a53-cd02-46ad-b136-dfa3751cff1e)](https://www.jianshu.com/mobile/campaign/day_by_day/join)

2020.04.22 20:36:55字数 2,259阅读 57

![img](https://upload-images.jianshu.io/upload_images/13638982-d2c910dab62d405c?imageMogr2/auto-orient/strip|imageView2/2/w/500)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

我一铁哥们从去年到今年先后面试了 4次美团，外卖、订单、商旅面试了好几个部门，终于在今年年初成功拿下offer，**总结下来各部门面试的大体思路基本都一致。比如：**

- JVM 参数配置、常用调试工具、分区、类加载，还会问你有需要线上的调试问题吗？遇到死循环 CPU 飙升怎么解决？
- Java 并发包常用工具用法和原理、会配合集合类一起考，对了还会有 volatile、CAS 原理等。
- MySQL 也算是必备了，索引存储结构、索引搜索原理、事务的隔离级别和原理，这些真的是逢考必问。当然除了 MySQL，Redis 和  ES 也是面试长文的，大多都是集中到原理。比如 ES 倒排索引、分片原理，Redis 的 zset 原理和使用场景、多路复用、穿透、熔断等等。
- 框架也是必备的知识点，最常见的就是 AOP 原理，自己怎么实现？Spring Boot 啥原理？框架通常会配合设计模式一起考，比如你最熟悉的设计模式是啥？Spring MVC 里面用了什么设计模式？解决了什么问题？
- 接下来最重要的就是服务治理了，这里面内容就太多了，Dubbo 也好，Spring Cloud 也罢，总之这个地方最能看得出你真实的工作经验和问题的考虑深度，毕竟没有真正在庞大的系统里面锻炼过真的很难应付这个地方。
- 没漏掉还有一个最重要的算法，这个就靠平时多练了，LeetCode 中文版上线了，一天一道题，面试必无敌。

说了这么多只有一个重点，就是无论大厂他有没有题库，**面试题的大体方向就这么多，你要都掌握了，还担心去大厂？**

# 那么重点就来了，怎么复习呢？

其实一步一步走过来，不单单只靠面试之前刷题那么简单，更多的还是平时的积累。**小编为金三银四面试的朋友整理出一篇Java进阶架构师之路的核心知识，同时也是面试时面试官必问的知识点，篇章也是包括了很多知识点，其中包括了有基础知识、Java集合、JVM、多线程并发、spring原理、微服务、Netty 与RPC 、Kafka、日记、设计模式、Java算法、数据库、Zookeeper、分布式缓存、数据结构等等**

# 1、JVM

- 垃圾回收算法有几种类型？ 他们对应的优缺点又是什么？
- 类的加载过程是什么？简单描述一下每个步骤
- JVM 预定义的类加载器有哪几种？分别什么作用？
- 什么是双亲委派模式？有什么作用？
- 什么是内存溢出， 内存泄露？ 他们的区别是什么？
- 引起类加载操作的行为有哪些？
- 介绍一下 JVM 提供的常用工具
- Full GC 、 Major GC 、Minor GC 之间区别？
- 什么时候触发 Full GC ？
   ...

# 2、Java并发

- 什么是可重入锁、乐观锁、悲观锁、公平锁、非公平锁、独占锁、共享锁？
- 讲讲ThreadLocal 的实现原理？
- ThreadLocal 作为变量的线程隔离方式，其内部是如何做的？
- 说说InheritableThreadLocal 的实现原理？
- 并发包中锁的实现底层（对AQS的理解）？
- 讲讲独占锁 ReentrantLock 原理？

![img](https://upload-images.jianshu.io/upload_images/13638982-0ce871bab960746f?imageMogr2/auto-orient/strip|imageView2/2/w/640)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

# 3、Java集合

- HashSet 和 TreeSet 有什么区别？
- HashSet 的底层实现是什么?
- LinkedHashMap 的实现原理?
- 为什么集合类没有实现 Cloneable 和 Serializable 接口？
- 什么是迭代器 (Iterator)？
- Iterator 和 ListIterator 的区别是什么？

![img](https://upload-images.jianshu.io/upload_images/13638982-45c7454914f19f60?imageMogr2/auto-orient/strip|imageView2/2/w/640)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

# 4、Spring全家桶

- Spring bean的生命周期能不能结合源码回答一下这个问题、或者结合一下bean的生命的意义来回答，就是Spring为什么需要找个生命周期
- Spring容器当中包含了哪些常用组件（至少说5个），作用是什么，场景是什么；比如BeanDefinition；再比如BeanDefinitionMap
- Spring自动注入的原理是什么？能不能从源码来说明一下这个问题；我们常常说的自动注入，到底怎么注入的？有什么坑？怎么让你一个属性不自动注入
- Spring源码当中如何来搞定循环依赖的？Spring支持循环依赖？生命情况不支持？支持的原理是什么？能不能从源码来说明一下？
- 如何来二次扩展Spring，比如自定义一个实现自动注入的注解；不使用@Autowried，自己如何开发一个@XXX来完成自动注入？
- mybatis源码当中利用了Spirng的那些扩展？mybatis扩展Spring之后有哪些问题是无法解决的？比如二级缓存怎么解决
- eureka源码当中如何扩展的Spring？比如怎么动态插拔eureka的功能，利用了Spring的那个技术点，或者从源码说一下

![img](https://upload-images.jianshu.io/upload_images/13638982-d8e9d0893ce0c6f6?imageMogr2/auto-orient/strip|imageView2/2/w/640)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

# 5、Redis

- Redis 持久化机制有哪些？ 区别是什么？优缺点是什么？
- Redis支持的数据类型
- 为什么 Redis 需要把所有数据放到内存中？
- Redis 是单线程的吗？
- Redis 的缓存失效策略有哪几种？
- 什么是缓存命中率？提高缓存命中率的方法有哪些？
- Redis全局命令及数据库管理
- Redis设计订单应用场景
- Redis缓存雪崩讲讲看？
- 什么是缓存穿透？
- Redis重启时加载AOF与RDB的顺序

![img](https://upload-images.jianshu.io/upload_images/13638982-33e1aca57cb4777a?imageMogr2/auto-orient/strip|imageView2/2/w/640)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

# 6、中间件

- Dubbo完整的一次调用链路介绍；
- Dubbo支持几种负载均衡策略？
- Dubbo Provider服务提供者要控制执行并发请求上限，具体怎么做？
- Dubbo启动的时候支持几种配置方式？
- 了解几种消息中间件产品？各产品的优缺点介绍；
- 消息中间件如何保证消息的一致性和如何进行消息的重试机制？
- Spring Cloud熔断机制介绍；
- Spring Cloud对比下Dubbo，什么场景下该使用Spring Cloud？

![img](https://upload-images.jianshu.io/upload_images/13638982-bc81a40a46cbb67c?imageMogr2/auto-orient/strip|imageView2/2/w/640)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

# 7、分布式

- 消息中间件如何解决消息丢失问题
- Dubbo的服务请求失败怎么处理
- 重连机制会不会造成错误
- 对分布式事务的理解
- 如何实现负载均衡，有哪些算法可以实现？
- Zookeeper的用途，选举的原理是什么？
- 数据的垂直拆分水平拆分。
- zookeeper原理和适用场景
- zookeeper watch机制
- redis/zk节点宕机如何处理
- 分布式集群下如何做到唯一序列号
- 如何做一个分布式锁
- 用过哪些MQ，怎么用的，和其他mq比较有什么优缺点，MQ的连接是线程安全的吗
- MQ系统的数据如何保证不丢失
- 列举出你能想到的数据库分库分表策略；分库分表后，如何解决全表查询的问题。

![img](https://upload-images.jianshu.io/upload_images/13638982-e78aef613a08c4c2?imageMogr2/auto-orient/strip|imageView2/2/w/640)

小伙四面美团终拿下Offer，全靠刷了这1000道互联网高频面试笔记

# 8、数据库

1. MySQL InnoDB存储的文件结构
2. 索引树是如何维护的？
3. 数据库自增主键可能的问题
4. MySQL的几种优化
5. mysql索引为什么使用B+树
6. 数据库锁表的相关处理
7. 索引失效场景
8. 高并发下如何做到安全的修改同一行数据，乐观锁和悲观锁是什么，INNODB的行级锁有哪2种，解释其含义
9. 数据库会死锁吗，举一个死锁的例子，mysql怎么解决死锁

