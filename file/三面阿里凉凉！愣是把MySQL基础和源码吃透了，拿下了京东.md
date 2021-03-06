# 三面阿里凉凉！愣是把MySQL基础和源码吃透了，拿下了京东

作为一名后端开发，MySQL是工作上最常用的关系型数据库之一。随着移动互联网的高速发展，集群架构已经成为主流趋势，对于数据库的高并发，高可用等指标的要求也越来越高。

应聘者是否具备相应的底层机制和原理的驾驭能力，成为互联网公司筛选人才的重要考核标准。如果你只停留在建库、创表、增删查该等基本操作水平，迟早会被企业淘汰。

举三个栗子（面试官常问）：

- 如何提高查询语句性能？
- 如何突破单库性能瓶颈？
- 如何做到数据库的高并发与高可用？

下面，为了避免大家刷题踩坑，我把MySQL**常见面试**给大家整理出了一份PDF文档，方便大家查漏补缺。

- **文档特点：条理清晰，图文结合，通俗易懂**
- **为了大家更好的阅读体验，在此每个知识点仅展示部分内容，如果你需要系统的学习这份文档的内容，点右方链接：[https://shimo.im/docs/QVy8HrQgPYkx9Ddg](https://links.jianshu.com/go?to=https%3A%2F%2Fshimo.im%2Fdocs%2FQVy8HrQgPYkx9Ddg)即可免费获取！**

# 一、数据库基础知识

**1、为什么要使用数据库**

![img](https://upload-images.jianshu.io/upload_images/22421829-4abee6ae82776cef?imageMogr2/auto-orient/strip|imageView2/2/w/553)

**2、什么是 SQL？**

结构化查询语言(Structured Query Language)简称 SQL，是一种数据库查询语言。

作用：用于存取数据、查询、更新和管理关系数据库系统。

**3、什么是 MySQL?**

MySQL 是一个关系型数据库管理系统，由瑞典 MySQL AB 公司开发，属于 Oracle 旗下

产品。MySQL 是最流行的关系型数据库管理系统之一，在 WEB 应用方面，MySQL 是最

好的 RDBMS (Relational Database Management System，关系数据库管理系统) 应用

软件之一。在 Java 企业级开发中非常常用，因为 MySQL 是开源免费的，并且方便扩展。

**4、........**

# 二、数据类型

**1、mysql 有哪些数据类型**

![img](https://upload-images.jianshu.io/upload_images/22421829-4005a8694021152b?imageMogr2/auto-orient/strip|imageView2/2/w/640)

# 三、引擎

**1、MySQL 存储引擎 MyISAM 与 InnoDB 区别**

存储引擎 Storage engine：MySQL 中的数据、索引以及其他对象是如何存储的，是一套

文件系统的实现。

**常用的存储引擎有以下：**

**Innodb 引擎：**Innodb 引擎提供了对数据库 ACID 事务的支持。并且还提供了行级锁

和外键的约束。它的设计的目标就是处理大数据容量的数据库系统。

**MyIASM 引擎：**(原本 Mysql 的默认引擎)：不提供事务的支持，也不支持行级锁和外键。

**MEMORY 引擎：**所有的数据都在内存中，数据的处理速度快，但是安全性不高。

**2、MyISAM 与 InnoDB 区别**

![img](https://upload-images.jianshu.io/upload_images/22421829-ed8853d3bf37e931?imageMogr2/auto-orient/strip|imageView2/2/w/640)

**3、InnoDB 引擎的 4 大特性**

- 插入缓冲（insert buffer)
- 二次写(double write)
- 自适应哈希索引(ahi)
- 预读(read ahead)

**4、存储引擎选择**

如果没有特别的需求，使用默认的 Innodb 即可。

MyISAM：以读写插入为主的应用程序，比如博客系统、新闻门户网站。

Innodb：更新（删除）操作频率也高，或者要保证数据的完整性；并发量高，支持事务和

外键。比如 OA 自动化办公系统。

# 四、索引

**1、什么是索引？**

**2、索引有哪些优缺点？**

**3、索引使用场景（重点）**

**4、索引有哪几种类型？**

**5、索引的数据结构（b 树，hash）**

**6、索引的基本原理**

**7、索引算法有哪些？**

**8、索引设计的原则？**

**9、创建索引的原则（重中之重）**

**10、创建索引的三种方式，删除索引**

**11、创建索引时需要注意什么？**

**12、使用索引查询一定能提高查询的性能吗？为什么？**

**13、百万级别或以上的数据如何删除**

**14、前缀索引**

**15、什么是最左前缀原则？什么是最左匹配原则**

**16、B 树和 B+树的区别**

**17、使用 B 树的好处**

**18、使用 B+树的好处**

**19、Hash 索引和 B+树所有有什么区别或者说优劣呢?**

**20、数据库为什么使用 B+树而不是 B 树**

**21、B+树在满足聚簇索引和覆盖索引的时候不需要回表查询数 据**

**22、什么是聚簇索引？何时使用聚簇索引与非聚簇索引？**

**23、联合索引是什么？为什么需要注意联合索引中的顺序？**

![img](https://upload-images.jianshu.io/upload_images/22421829-9ac4b324e1a4cf83?imageMogr2/auto-orient/strip|imageView2/2/w/640)

![img](https://upload-images.jianshu.io/upload_images/22421829-9bfba4d66ae4f931?imageMogr2/auto-orient/strip|imageView2/2/w/640)

![img](https://upload-images.jianshu.io/upload_images/22421829-ba1baa1572bb2a42?imageMogr2/auto-orient/strip|imageView2/2/w/640)

# 五、事务

**1、什么是数据库事务？**

**2、事物的四大特性(ACID)介绍一下?**

**3、什么是脏读？幻读？不可重复读？**

**4、什么是事务的隔离级别？MySQL 的默认隔离级别是什么？**

![img](https://upload-images.jianshu.io/upload_images/22421829-8e4e08dc40743d75?imageMogr2/auto-orient/strip|imageView2/2/w/640)

# 六、锁

**1、对 MySQL 的锁了解吗**

当数据库有并发事务的时候，可能会产生数据的不一致，这时候需要一些机制来保证访问的次序，锁机制就是这样的一个机制。

就像酒店的房间，如果大家随意进出，就会出现多人抢夺同一个房间的情况，而在房间上装上锁，申请到钥匙的人才可以入住并且将房间锁起来，其他人只有等他使用完毕才可以再次使用。

**2、隔离级别与锁的关系**

**3、按照锁的粒度分数据库锁有哪些？锁机制与 InnoDB 锁算法**

**4、什么是死锁？怎么解决？**

死锁是指两个或多个事务在同一资源上相互占用，并请求锁定对方的资源，从而导致恶性循环的现象。

**常见的解决死锁的方法：**

1、如果不同程序会并发存取多个表，尽量约定以相同的顺序访问表，可以大大降低死锁机

会。

2、在同一个事务中，尽可能做到一次锁定所需要的所有资源，减少死锁产生概率；

3、对于非常容易产生死锁的业务部分，可以尝试使用升级锁定颗粒度，通过表级锁定来减

少死锁产生的概率；

如果业务处理不好可以用分布式事务锁或者使用乐观锁

**5、.......**

![img](https://upload-images.jianshu.io/upload_images/22421829-cbaae5299dfd0e44?imageMogr2/auto-orient/strip|imageView2/2/w/640)

# 七、视图

**1、为什么要使用视图？什么是视图？**

为了提高复杂 SQL 语句的复用性和表操作的安全性，MySQL 数据库管理系统提供了视图

特性。所谓视图，本质上是一种虚拟表，在物理上是不存在的，其内容与真实的表相似，包

含一系列带有名称的列和行数据。但是，视图并不在数据库中以储存的数据值形式存在。行

和列数据来自定义视图的查询所引用基本表，并且在具体引用视图时动态生成。

视图使开发者只关心感兴趣的某些特定数据和所负责的特定任务，只能看到视图中所定义的

数据，而不是视图所引用表中的数据，从而提高了数据库中数据的安全性。

**2、视图有哪些特点？**

- 视图的列可以来自不同的表，是表的抽象和在逻辑意义上建立的新关系。
- 视图是由基本表(实表)产生的表(虚表)。
- 视图的建立和删除不影响基本表。
- 对视图内容的更新(添加，删除和修改)直接影响基本表。
- 当视图来自多个基本表时，不允许添加和删除数据。

视图的操作包括创建视图，查看视图，删除视图和修改视图。

**3、视图的使用场景有哪些？**

视图根本用途：简化 sql 查询，提高开发效率。如果说还有另外一个用途那就是兼容老的表

结构。

**下面是视图的常见使用场景：**

- 重用 SQL 语句；
- 简化复杂的 SQL 操作。在编写查询后，可以方便的重用它而不必知道它的基本查询细节；
- 使用表的组成部分而不是整个表；
- 保护数据。可以给用户授予表的特定部分的访问权限而不是整个表的访问权限；
- 更改数据格式和表示。视图可返回与底层表的表示和格式不同的数据。

**4、.....**

# 八、存储过程与函数

**1、什么是存储过程？有哪些优缺点？**

存储过程是一个预编译的 SQL 语句，优点是允许模块化的设计，就是说只需要创建一次，

以后在该程序中就可以调用多次。如果某次操作需要执行多次 SQL，使用存储过程比单纯

SQL 语句执行要快。

**优点：**

1）存储过程是预编译过的，执行效率高。

2）存储过程的代码直接存放于数据库中，通过存储过程名直接调用，减少网络通讯。

3）安全性高，执行存储过程需要有一定权限的用户。

4）存储过程可以重复使用，减少数据库开发人员的工作量。

**缺点：**

1）调试麻烦，但是用 PL/SQL Developer 调试很方便！弥补这个缺点。

2）移植问题，数据库端代码当然是与数据库相关的。但是如果是做工程型项目，基本不存

在移植问题。

3）重新编译问题，因为后端代码是运行前编译的，如果带有引用关系的对象发生改变时，

受影响的存储过程、包将需要重新编译（不过也可以设置成运行时刻自动编译）。

4）如果在一个程序系统中大量的使用存储过程，到程序交付使用的时候随着用户需求的增

加会导致数据结构的变化，接着就是系统的相关问题了，最后如果用户想维护该系统可以说

是很难很难、而且代价是空前的，维护起来更麻烦。