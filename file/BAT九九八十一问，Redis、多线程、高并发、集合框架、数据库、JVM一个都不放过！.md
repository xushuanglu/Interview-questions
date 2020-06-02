# BAT九九八十一问，Redis、多线程、高并发、集合框架、数据库、JVM一个都不放过！



### 第一弹：Redis

1. 为什么要用 redis /为什么要用缓存（高性能、高并发）
2. 为什么要用 redis 而不用 map/guava 做缓存?
3. redis 常见数据结构以及使用场景分析（String、Hash、List、Set、Sorted Set）
4. redis 内存淘汰机制（MySQL里有2000w数据，Redis中只存20w的数据，如何保证Redis中的数据都是热点数据？）
5. redis 持久化机制（怎么保证 redis 挂掉之后再重启数据可以进行恢复）
6. Redis 常见异常及解决方案（缓存穿透、缓存雪崩、缓存预热、缓存降级）
7. 分布式环境下常见的应用场景（分布式锁、分布式自增 ID）
8. Redis 集群模式（主从模式、哨兵模式、Cluster 集群模式）
9. 如何解决 Redis 的并发竞争 Key 问题
10. 如何保证缓存与数据库双写时的数据一致性？

### 第二弹：多线程/高并发

1. stop() 和 suspend() 方法为何不推荐使用？
2. sleep() 和 wait() 有什么区别?
3. 同步和异步有何异同，在什么情况下分别使用他们？
4. 当一个线程进入一个对象的一个 synchronized 方法后，其它线程是否可进入此对象的其它方法?
5. 简述 synchronized 和 java.util.concurrent.locks.Lock 的异同？
6. 概括的解释下线程的几种可用状态。
7. 什么是 ThreadLocal?
8. run() 和 start() 区别。
9. 什么是线程饿死，什么是活锁？
10. 请说出你所知道的线程同步的方法。
11. 线程调度和线程控制。
12. 多线程中的忙循环是什么?
13. volatile 变量是什么？volatile 变量和 atomic 变量有什么不同？
14. volatile 类型变量提供什么保证？能使得一个非原子操作变成原子操作吗？

### 第三弹：集合框架

1. ArrayList 和 Vector 的区别
2. 说说 ArrayList,Vector, LinkedList 的存储性能和特性。
3. 快速失败 (fail-fast) 和安全失败 (fail-safe) 的区别是什么？
4. hashmap 的数据结构。
5. HashMap 的工作原理是什么?
6. Hashmap 什么时候进行扩容呢？
7. List、Map、Set 三个接口，存取元素时，各有什么特点？
8. Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢? 是用 == 还是equals()? 它们有何区别?
9. 两个对象值相同 (x.equals(y) == true)，但却可有不同的 hash code，这句话对不对?
10. heap 和 stack 有什么区别
11. Java 集合类框架的基本接口有哪些？
12. HashSet 和 TreeSet 有什么区别？
13. HashSet 的底层实现是什么?
14. LinkedHashMap 的实现原理?
15. 为什么集合类没有实现 Cloneable 和 Serializable 接口？
16. 什么是迭代器 (Iterator)？
17. Iterator 和 ListIterator 的区别是什么？
18. 数组 (Array) 和列表 (ArrayList) 有什么区别？什么时候应该使用 Array 而不是ArrayList？
19. Java 集合类框架的最佳实践有哪些？
20. Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢？是用 == 还是equals()？它们有何区别？
21. Comparable 和 Comparator 接口是干什么的？列出它们的区别。
22. Collection 和 Collections 的区别。

### 第四弹：数据库

1. 请简洁描述 MySQL 中 InnoDB 支持的四种事务隔离级别名称，以及逐级之间的区别？
2. 在 MySQL 中 ENUM 的用法是什么？
3. CHAR 和 VARCHAR 的区别？
4. 列的字符串类型可以是什么？
5. MySQL 中使用什么存储引擎？
6. TIMESTAMP 在 UPDATE CURRENT_TIMESTAMP 数据类型上做什么？
7. 主键和候选键有什么区别？
8. MySQL 数据库服务器性能分析的方法命令有哪些?
9. LIKE 和 REGEXP 操作有什么区别？
10. BLOB 和 TEXT 有什么区别？
11. 数据库的三范式？
12. 什么是通用 SQL 函数？
13. MySQL 表中允许有多少个 TRIGGERS？

### 第五弹：JVM

1. Java 类加载过程？
2. 描述一下 JVM 加载 Class 文件的原理机制?
3. Java 内存分配。
4. GC 是什么? 为什么要有 GC？
5. 简述 Java 垃圾回收机制。
6. 如何判断一个对象是否存活？（或者 GC 对象的判定方法）
7. 垃圾回收的优点和原理。并考虑 2 种回收机制。
8. 垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？
9. 有什么办法主动通知虚拟机进行垃圾回收？
10. Java 中会存在内存泄漏吗，请简单描述。
11. 深拷贝和浅拷贝。
12. System.gc() 和 Runtime.gc() 会做什么事情？
13. finalize() 方法什么时候被调用？析构函数 (finalization) 的目的是什么？
14. 如果对象的引用被置为 null，垃圾收集器是否会立即释放对象占用的内存？
15. 什么是分布式垃圾回收（DGC）？它是如何工作的？
16. 串行（serial）收集器和吞吐量（throughput）收集器的区别是什么？
17. 在 Java 中，对象什么时候可以被垃圾回收？
18. 简述 Java 内存分配与回收策率以及 Minor GC 和 Major GC。
19. JVM 的永久代中会发生垃圾回收么？
20. Java 中垃圾收集的方法有哪些？
21. 什么是类加载器，类加载器有哪些？
22. 类加载器双亲委派模型机制？

倘若不看答案，上面的81问你能答对多少呢？



![img](https://upload-images.jianshu.io/upload_images/18375227-af588823e6f1cab8.png?imageMogr2/auto-orient/strip|imageView2/2/w/201)

image.png

> 由于答案都是以截图展示的，如果觉得图片不方便或者清晰度不高的话，可以[【点击看答案】](https://links.jianshu.com/go?to=https%3A%2F%2Fshimo.im%2Fdocs%2FQ8vTXyKytkkqvQkc%2F)下载完整的原文档！

# 看答案看答案...

### 第五弹：JVM答案

![img](https://upload-images.jianshu.io/upload_images/18375227-9ff34b7af1a37587.png?imageMogr2/auto-orient/strip|imageView2/2/w/1190)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-f08f3669b8371cbf.png?imageMogr2/auto-orient/strip|imageView2/2/w/1154)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-2c869edc833a3129.png?imageMogr2/auto-orient/strip|imageView2/2/w/1190)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-14e07460406f323d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1170)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-8a1e168ac81e8077.png?imageMogr2/auto-orient/strip|imageView2/2/w/1132)

image.png

### 第四弹：数据库

![img](https://upload-images.jianshu.io/upload_images/18375227-f93e6cc6e2e6a621.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-d21cd8541609cd89.png?imageMogr2/auto-orient/strip|imageView2/2/w/1164)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-d7d87f00064ddb7e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1181)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-fae55a3324e16a48.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-a6f471d56240531f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png

### 第三弹：集合框架

![img](https://upload-images.jianshu.io/upload_images/18375227-6f2c16b039f4e4c7.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-72b3b228739dee0e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-101910e9acf4e2fe.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-52e00dcd4782666a.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-125d6433d761bb07.png?imageMogr2/auto-orient/strip|imageView2/2/w/1189)

image.png

### 第二弹：多线程/高并发

![img](https://upload-images.jianshu.io/upload_images/18375227-531c2afed584aa75.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-8a3bf24bae4becc4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-75bee9f66f57e290.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-97f77904c7476013.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-a4232b730b779cec.png?imageMogr2/auto-orient/strip|imageView2/2/w/601)

image.png

### 第一弹：Redis

![img](https://upload-images.jianshu.io/upload_images/18375227-6657df0017ce31fd.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-a41d234971321186.png?imageMogr2/auto-orient/strip|imageView2/2/w/619)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-b7161395e0f98eb1.png?imageMogr2/auto-orient/strip|imageView2/2/w/590)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-c12d449205afcd53.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-adc9f34dbfc83df2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-27f635773d22b9b1.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png



![img](https://upload-images.jianshu.io/upload_images/18375227-ce244f853ad8617e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

image.png

> 更多关于Java集合、JVM、多线程并发、spring原理、微服务、Netty 与RPC 、Kafka、日记、设计模式、Java算法、数据库、Zookeeper、分布式缓存、数据结构面试解析等等可以去这个Github链接地址：**[https://github.com/ThinkingHan/Java-note](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FThinkingHan%2FJava-note)**阅读，Star一下吧，感谢支持~

"小礼物走一走，来简书关注我"

还没有人赞赏，支持一下

[![  ](https://upload.jianshu.io/users/upload_avatars/18375227/eb7d73d5-2b66-4fde-af00-2d3b2076ce8e.png?imageMogr2/auto-orient/strip|imageView2/1/w/100/h/100)](https://www.jianshu.com/u/5872afeb0215)

[java菲](https://www.jianshu.com/u/5872afeb0215)现在加群号：578486082 即可获取Java工程化、高性能及分布式、高性能、高架构。性能调...

总资产458 (约49.16元)共写了92.1W字获得4,246个赞共10,863个粉丝



### 被以下专题收入，发现更多相似内容

[![img](https://upload.jianshu.io/collections/images/1804025/RDJ.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48)老男孩的成长之路](https://www.jianshu.com/c/88d27e431b8a)[![img](https://upload.jianshu.io/collections/images/1723071/6a77219acc35e56c39226b0e2f959a57.png?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48)Java架构技术进阶](https://www.jianshu.com/c/8d050bf89c61)[![img](https://upload.jianshu.io/collections/images/15611/java.png?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48)Java](https://www.jianshu.com/c/cc4a77142aa4)[![img](https://upload.jianshu.io/collections/images/919/keji.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48)互联网科技](https://www.jianshu.com/c/93d58e9169cb)

![img](https://oimagea7.ydstatic.com/image?id=2223816700015246366&product=adpublish&w=520&h=347)广告

[![img](https://upload.jianshu.io/users/upload_avatars/18375227/eb7d73d5-2b66-4fde-af00-2d3b2076ce8e.png?imageMogr2/auto-orient/strip|imageView2/1/w/90/h/90)](https://www.jianshu.com/u/5872afeb0215)

[java菲](https://www.jianshu.com/u/5872afeb0215)

总资产458 (约49.16元)

[看完这篇 Session、Cookie、Token，和面试官扯皮就没问题了](https://www.jianshu.com/p/4cd7b0915cd2)

阅读 295

[面试官问单例设计模式，问问你自己真的了解吗？小单例，不简单！](https://www.jianshu.com/p/7ae1e99da25b)

阅读 41

[MySQL性能优化21个最佳实践，一个一个分解给你看，还怕搞不定？](https://www.jianshu.com/p/5ea10f287607)

阅读 45

### 推荐阅读

[面试问我，创建多少个线程合适？我该怎么说](https://www.jianshu.com/p/f30ee2346f9f)

阅读 17,467

[因用了Insert into select语句，同事被开除了！](https://www.jianshu.com/p/88c58a09f95a)

阅读 993

[如何成为写SQL高手（下）](https://www.jianshu.com/p/5c6305c9c099)

阅读 4,029

[一款SQL自动检查神器，再也不用担心SQL出错了，自动补全、回滚等功能大全](https://www.jianshu.com/p/099a9282229c)

阅读 1,611

[开源MySQL_Monito 图形可视化监控工具](https://www.jianshu.com/p/c9ab1c2f4c6d)

阅读 547

![img](https://oimagea1.ydstatic.com/image?id=-3368319885275975218&product=adpublish&w=520&h=347)广告