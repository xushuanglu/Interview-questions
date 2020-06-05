# 24岁程序员小伙,轻松拿下美团/滴滴/苏宁offer,只因看完了这个PDF

[![img](https://upload.jianshu.io/users/upload_avatars/13638982/22c4c181-49bf-48e7-bbcf-608d5cad9541.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96)](https://www.jianshu.com/u/4a35811f38e1)

[慕容千语](https://www.jianshu.com/u/4a35811f38e1)[![  ](https://upload.jianshu.io/user_badge/ec7b4a53-cd02-46ad-b136-dfa3751cff1e)](https://www.jianshu.com/mobile/campaign/day_by_day/join)

22020.03.21 13:59:01字数 2,853阅读 266

> 本文作者：晓风残月
>
> 本文来源：微信公众号
>  **欢迎关注专栏：[Java架构技术进阶](https://www.jianshu.com/c/8d050bf89c61)。里面有大量batj面试题集锦，还有各种技术分享，如有好文章也欢迎投稿哦。**

今年突发疫情打乱了我的安排，原计划春节一结束就可以出去找工作，突如其来的禁足让我计划泡汤，最主要的是年前还辞职了，在家三个月期间没有任何收入，不过也不能说完全没有收获，三个月时间我也没有完全浪费，在年前刷到了一篇很不错的文章，有分享一些面试经验和面试真题，在家期间就把这些刷完了。

然后在接下来的三月初，面试电话打来了，因疫情原因，选择视频面试，在经历三轮面试之后，拿下了苏宁offer，后面几天连续接到美团，滴滴等电话面试，有幸全部通过。其中美团面试差一点翻车面试官是一问接一问问道我答不上来才截止，估计这也是为了探探我的技术深度。

大家是不是很好奇究竟是哪些面试真题和面试经验让我收获如此丰富。下面我为大家揭晓这些整理文档里面的部分知识点。

![img](https://upload-images.jianshu.io/upload_images/13638982-53c184f091bb9bf9?imageMogr2/auto-orient/strip|imageView2/2/w/640)

##### 并发编程：

1. 什么是多线程并发和并行？
2. 什么是线程安全问题？
3. 什么是共享变量的内存可见性问题？
4. 什么是Java中原子性操作？
5. 什么是Java中的CAS操作,AtomicLong实现原理？
6. 什么是Java指令重排序？
7. Java中Synchronized关键字的内存语义是什么？
8. Java中Volatile关键字的内存语义是什么？
9. 什么是伪共享,为何会出现，以及如何避免？
10. 什么是可重入锁、乐观锁、悲观锁、公平锁、非公平锁、独占锁、共享锁？
11. 讲讲ThreadLocal 的实现原理？
12. ThreadLocal 作为变量的线程隔离方式，其内部是如何做的？
13. 说说InheritableThreadLocal 的实现原理？
14. InheritableThreadLocal 是如何弥补 ThreadLocal 不支持继承的特性？
15. CyclicBarrier内部的实现与 CountDownLatch 有何不同？
16. 随机数生成器 Random 类如何使用 CAS 算法保证多线程下新种子的唯一性？
17. ThreadLocalRandom 是如何利用 ThreadLocal 的原理来解决 Random 的局限性？
18. Spring 框架中如何使用 ThreadLocal 实现 request scope 作用域 Bean？
19. 并发包中锁的实现底层（对AQS的理解）？
20. 讲讲独占锁 ReentrantLock 原理？
21. 谈谈读写锁 ReentrantReadWriteLock 原理？
22. StampedLock 锁原理的理解？
23. 谈下对基于链表的非阻塞无界队列 ConcurrentLinkedQueue 原理的理解？
24. ConcurrentLinkedQueue 内部是如何使用 CAS 非阻塞算法来保证多线程下入队出队操作的线程安全？
25. 基于链表的阻塞队列 LinkedBlockingQueue 原理。
26. 阻塞队列LinkedBlockingQueue 内部是如何使用两个独占锁 ReentrantLock 以及对应的条件变量保证多线程先入队出队操作的线程安全？
27. 分析下JUC 中倒数计数器 CountDownLatch 的使用与原理？
28. CountDownLatch 与线程的 Join 方法区别是什么？
29. 讲讲对JUC 中回环屏障 CyclicBarrier 的使用？
30. CyclicBarrier内部的实现与 CountDownLatch 有何不同？
31. Semaphore 的内部实现是怎样的？
32. 并发组件CopyOnWriteArrayList 是如何通过写时拷贝实现并发安全的 List？

![img](https://upload-images.jianshu.io/upload_images/13638982-737b92a867d22547?imageMogr2/auto-orient/strip|imageView2/2/w/640)

##### JVM

1. Java 内存分配？
2. Java 堆的结构是什么样子的？
3. 什么是堆中的永久代（Perm Gen space）?
4. 说说各个区域的作用？
5. Java 中会存在内存泄漏吗，简述一下？
6. Java 类加载过程？
7. 描述一下 JVM 加载 Class 文件的原理机制?
8. 什么是类加载器？
9. 类加载器有哪些？
10. 什么是tomcat类加载机制？
11. 类加载器双亲委派模型机制？
12. 什么是GC? 为什么要有 GC？
13. 简述一下Java 垃圾回收机制？
14. 如何判断一个对象是否存活？
15. 垃圾回收的优点和原理，并考虑 2 种回收机制？
16. 垃圾回收器的基本原理是什么？
17. 垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？
18. 深拷贝和浅拷贝？
19. System.gc() 和 Runtime.gc() 会做些什么？
20. 什么是分布式垃圾回收（DGC）？它是如何工作的？
21. 串行（serial）收集器和吞吐量（throughput）收集器的区别是什么？
22. 在 Java 中，对象什么时候可以被垃圾回收？
23. 简述Minor GC 和 Major GC？
24. Java 中垃圾收集的方法有哪些？
25. 讲讲你理解的性能评价及测试指标？
26. 常用的性能优化方式有哪些？
27. 说说分布式缓存和一致性哈希？
28. 同步与异步？阻塞与非阻塞？
29. 什么是GC调优？
30. 常见异步的手段有哪些？

##### Spring

1. 为什么需要代理模式？
2. 讲讲静态代理模式的优点及其瓶颈？
3. 对Java 接口代理模式的实现原理的理解？
4. 如何使用 Java 反射实现动态代理？
5. Java 接口代理模式的指定增强？
6. 谈谈对Cglib 类增强动态代理的实现？
7. 怎么理解面向切面编程的切面？
8. 讲解OOP与AOP的简单对比？
9. 讲解JDK 动态代理和 CGLIB 代理原理以及区别？
10. 讲解Spring 框架中基于 Schema 的 AOP 实现原理？
11. 讲解Spring 框架中如何基于 AOP 实现的事务管理？
12. 谈谈对控制反转的设计思想的理解？
13. 怎么理解 Spring IOC 容器？
14. Spring IOC 怎么管理 Bean 之间的依赖关系，怎么避免循环依赖？
15. 对Spring IOC 容器的依赖注入的理解？
16. 说说对Spring IOC 的单例模式和高级特性？
17. BeanFactory 和 FactoryBean 有什么区别？
18. BeanFactory 和 ApplicationContext 又有什么不同？
19. Spring 在 Bean 创建过程中是如何解决循环依赖的？
20. 谈谈Spring Bean 创建过程中的设计模式？

##### 数据库

1. MySQL 有哪些存储引擎啊？都有什么区别？
2. Float、Decimal 存储金额的区别？
3. Datetime、Timestamp 存储时间的区别？
4. Char、Varchar、Varbinary 存储字符的区别？
5. 对比一下B+树索引和 Hash索引？
6. MySQL索引类型有？
7. 如何管理 MySQL索引？
8. 对Explain参数及重要参数的理解？
9. 索引利弊是什么及索引分类？
10. 聚簇索引和非聚簇索引的区别？
11. B+tree 如何进行优化？索引遵循哪些原则？
12. 索引与锁有什么关系？
13. 还有什么其他的索引类型，各自索引有哪些优缺点？
14. 谈谈对Innodb事务的理解？
15. 说说数据库事务特点及潜在问题？
16. 什么是MySQL隔离级别？
17. 有多少种事务失效的场景，如何解决？
18. 一致性非锁定读和一致性锁定读是什么？
19. Innodb如何解决幻读？
20. 讲讲Innodb行锁？
21. 死锁及监控是什么？
22. 自增长与锁 ，锁的算法，锁问题，锁升级是什么？
23. 乐观锁的线程如何做失败补偿？
24. 高并发场景（领红包）如何防止死锁，保证数据一致性？
25. 谈谈MySQL的锁并发？
26. 查询优化的基本思路是什么？
27. 说说MySQL读写分离、分库分表？
28. 表结构对性能有什么影响?
29. 浅谈索引优化？
30. 说说Sql优化的几点原则？
31. MySQL表设计及规范？
32. 说说MySQL几种存储引擎应用场景？
33. MySQL常用优化方式有哪些？
34. MySQL常用监控？
35. MySQL瓶颈分析？

##### 缓存

1. redis数据结构有哪些？
2. Redis缓存穿透，缓存雪崩？
3. 如何使用Redis来实现分布式锁？
4. Redis的并发竞争问题如何解决？
5. Redis持久化的几种方式，优缺点是什么，怎么实现的？
6. Redis的缓存失效策略？
7. Redis集群，高可用，原理？
8. Redis缓存分片？
9. Redis的数据淘汰策略？
10. redis队列应用场景？
11. 分布式使用场景（储存session）？

##### 网络编程

1. TCP建立连接和断开连接的过程？
2. HTTP协议的交互流程，HTTP和HTTPS的差异，SSL的交互流程？
3. TCP的滑动窗口协议有什么用？
4. HTTP协议都有哪些方法？
5. Socket交互的基本流程？
6. 讲讲tcp协议（建连过程，慢启动，滑动窗口，七层模型）？
7. webservice协议（wsdl/soap格式，与restt协议的区别）？
8. 说说Netty线程模型，什么是零拷贝？
9. TCP三次握手、四次挥手？
10. DNS解析过程？
11. TCP如何保证数据的可靠传输的？

##### 分布式

1. 什么是CAP定理？
2. 说说CAP理论和BASE理论？
3. 什么是最终一致性？最终一致性实现方式？
4. 什么是一致性Hash？
5. 讲讲分布式事务？
6. 如何实现分布式锁？
7. 如何实现分布式 Session?
8. 如何保证消息的一致性?
9. 负载均衡的理解？
10. 正向代理和反向代理？
11. CDN实现原理？
12. 怎么提升系统的QPS和吞吐？
13. Dubbo的底层实现原理和机制？
14. 描述一个服务从发布到被消费的详细过程？
15. 分布式系统怎么做服务治理？
16. 消息中间件如何解决消息丢失问题？
17. Dubbo的服务请求失败怎么处理？
18. 对分布式事务的理解？
19. 如何实现负载均衡,有哪些算法可以实现?
20. Zookeeper的用途,选举的原理是什么?
21. 讲讲数据的垂直拆分水平拆分？
22. zookeeper原理和适用场景？
23. zookeeper watch机制？
24. redis/zk节点宕机如何处理？
25. 分布式集群下如何做到唯一序列号？
26. 用过哪些MQ,怎么用的,和其他mq比较有什么优缺点,MQ的连接是线程安全的吗？
27. MQ系统的数据如何保证不丢失？
28. 列举出能想到的数据库分库分表策略？

以上就是部分展示，因文档内容太多，无法全部展示，如果需要可点击关键词“**[面试](https://links.jianshu.com/go?to=https%3A%2F%2Fjq.qq.com%2F%3F_wv%3D1027%26k%3D5ZOXo5Y)**”获取文档地址。

**Java高级工程师核心面试1080题解析**

![img](https://upload-images.jianshu.io/upload_images/13638982-1ff49a118d0f04f2?imageMogr2/auto-orient/strip|imageView2/2/w/640)

**Java高级架构面试知识点问题解析整理**

![img](https://upload-images.jianshu.io/upload_images/13638982-0013dd10ba10c659?imageMogr2/auto-orient/strip|imageView2/2/w/640)

**Java面试知识点笔记整理**

![img](https://upload-images.jianshu.io/upload_images/13638982-f5393e09a8da1519?imageMogr2/auto-orient/strip|imageView2/2/w/640)

**欢迎关注专栏：[Java架构技术进阶](https://www.jianshu.com/c/8d050bf89c61)。里面有大量batj面试题集锦，还有各种技术分享，如有好文章也欢迎投稿哦。**