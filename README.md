## 面试问题



### JVM面试题

- Javs中会存在内存泄漏吗，请简单描述。
    内存泄漏是指不再被使用的对象或者变量一直被占据在内存中。
    理论上来说，Java是有GC垃圾回收机制的，也就是说，不再被使用的对象，会被GC自动回收掉，自动从内存中清除。

    但是，即使这样，Java也还是存在着内存泄漏的情况，
        1、长生命周期的对象持有短生命周期对象的引用就很可能发生内存泄露。

        尽管短生命周期对象已经不再需要，但是因为长生命周期对象持有它的引用而导致不能被回收，这就是Java中内存泄露的发生场景，通俗地说，就是程序员可能创建了一个对象，以后一直不再使用这个对象，这个对象却一直被引用，即这个对象无用但是却无法被垃圾回收器回收的，这就是Java中可能出现内存泄露的情况，例如，缓存系统，我们加载了一个对象放在缓存中(例如放在一个全局map对象中)，然后一直不再使用它，这个对象一直被缓存引用，但却不再被使用。

        检查java中的内存泄露，一定要让程序将各种分支情况都完整执行到程序结束，然后看某个对象是否被使用过，如果没有，则才能判定这个对象属于内存泄露。

        如果一个外部类的实例对象的方法返回了一个内部类的实例对象，这个内部类对象被长期引用了，即使那个外部类实例对象不再被使用，但由于内部类持久外部类的实例对象，这个外部类对象将不会被垃圾回收，这也会造成内存泄露。

        2、当一个对象被存储进HashSet集合中以后，就不能修改这个对象中的那些参与计算哈希值的字段了，否则，对象修改后的哈希值与最初存储进HashSet集合中时的哈希值就不同了，在这种情况下，即使在contains方法使用该对象的当前引用作为的参数去HashSet集合中检索对象，也将返回找不到对象的结果，这也会导致无法从HashSet集合中单独删除当前对象，造成内存泄露

- Serial与Parallel GC之间的不同之处?
- 32位和64位的JMM; int类型变量的长度是多数?
- Java中WeakReference 与SoftReference 的区别?
- JVM选项-XX: +IUseCompressed0ops有什么作用?为什么要使用
- 怎祥通过Java 程序来判断JyM是32位还是64位?
- 32位JVM和64位JM的最大堆内存分别是多数?
- JhE、JDK、JVM及JIT之间有什么不同?
- 解释Java堆空间及GC?
- JM内存区域
- 程序计数器(线程私有)
- 虚拟机栈线程私有)
- 本地方法区(线程私有)
- 你能保证GC执行吗?
- 怎么获取Java程序使用的内存?堆使用的百分比?
- Java中堆和栈有什么区别?
- 描述一下JyM加载class文件的原理机制
- GC是什么?为什么要有GC?
- 堆(Heap-线程共享)运行时数据区
- 方法区/永久代(线程共享)
- JVM运行时内存
- 新生代
- 老年代
- 永欢代
- JAVA8与元数据
- 引用计数法
- 可达性分析
- 标记清除算法( Mark -Sweep)
- 复制算法( copying)
- 标记整理算法0M ark Compact)
- 分代收集算法
- 新生代与复制算法
- 老年代与标记复制算法
- JAVA强引用
- JAVA软引用


### spring面试题

1、不同版本的 Spring Framework 有哪些主要功能？
2、什么是 Spring Framework？
3、列举 Spring Framework 的优点。
4、Spring Framework 有哪些不同的功能？
5、Spring Framework 中有多少个模块，它们分别是什么？
6、什么是 Spring 配置文件？
7、Spring 应用程序有哪些不同组件？
8、使用 Spring 有哪些方式？
9、什么是 Spring IOC 容器？
10、什么是依赖注入？
11、可以通过多少种方式完成依赖注入？
12、区分构造函数注入和 setter 注入
13、spring 中有多少种 IOC 容器？
14、区分 BeanFactory 和 ApplicationContext。
15、列举 IoC 的一些好处。
16、Spring IoC 的实现机制。
17、什么是 spring bean？
18、spring 提供了哪些配置方式？
19、spring 支持集中 bean scope？
20、spring bean 容器的生命周期是什么样的？
21、什么是 spring 的内部 bean？
22、什么是 spring 装配
23、自动装配有哪些方式？
24、自动装配有什么局限？
25、什么是基于注解的容器配置
26、如何在 spring 中启动注解装配？
27、@Component, @Controller, @Repository
28、@Required 注解有什么用？
29、@Autowired 注解有什么用？
30、@Qualififier 注解有什么用？
31、@RequestMapping 注解有什么用？
32、spring DAO 有什么用？
33、列举 Spring DAO 抛出的异常。
34、spring JDBC API 中存在哪些类？
35、使用 Spring 访问 Hibernate 的方法有哪些？
36、列举 spring 支持的事务管理类型
37、spring 支持哪些 ORM 框架
38、什么是 AOP？
39、什么是 Aspect？
40、什么是切点（JoinPoint）
41、什么是通知（Advice）？
42、有哪些类型的通知（Advice）？
43、指出在 spring aop 中 concern 和 cross-cuttingconcern 的不同之处。
44、AOP 有哪些实现方式？
45、Spring AOP and AspectJ AOP 有什么区别？
46、如何理解 Spring 中的代理？
47、什么是编织（Weaving）？
48、Spring MVC 框架有什么用？
49、描述一下 DispatcherServlet 的工作流程
50、介绍一下 WebApplicationContext
51、什么是 spring?
52、使用 Spring 框架的好处是什么？
53、Spring 由哪些模块组成?
54、Spring的IOC和AOP机制
55、Spring中Autowired和Resource关键字的区别
56、依赖注入的方式有几种，各是什么?
57、讲一下什么是Spring
58、Spring MVC流程
59、springMVC是什么
60、SpringMVC怎么样设定重定向和转发的？
61、SpringMVC常用的注解有哪些
62、Spring的AOP理解
63、Spring的IOC理解
64、解释一下spring bean的生命周期
65、解释Spring支持的几种bean的作用域。
66、Spring基于xml注入bean的几种方式
67、Spring框架中都用到了哪些设计模式
68、核心容器（应用上下文) 模块
69、BeanFactory – BeanFactory 实现举例。
70、XMLBeanFactory
71、解释 AOP 模块
72、解释 JDBC 抽象和 DAO 模块
72、解释对象/关系映射集成模块。
73、解释 WEB 模块。
74、Spring 配置文件
75、什么是 Spring IOC 容器？
76、IOC 的优点是什么？
77、ApplicationContext 通常的实现是什么?
78、Bean 工厂和 Application contexts 有什么区别？
79、一个 Spring 的应用看起来象什么？
80、什么是 Spring 的依赖注入？
81、有哪些不同类型的 IOC（依赖注入）方式？
82、哪种依赖注入方式你建议使用，构造器注入，还是 Setter方法注入？
83、什么是 Spring beans?
84、一个 Spring Bean 定义 包含什么？
85、如何给 Spring 容器提供配置元数据?
86、你怎样定义类的作用域?
87、解释 Spring 支持的几种 bean 的作用域。
88、Spring 框架中的单例 bean 是线程安全的吗?
89、解释 Spring 框架中 bean 的生命周期
90、哪些是重要的 bean 生命周期方法？你能重载它们吗？
91、什么是 Spring 的内部 bean？
92、在 Spring 中如何注入一个 java 集合？
93、什么是 bean 装配?
94、什么是 bean 的自动装配？
95、解释不同方式的自动装配 。
96、自动装配有哪些局限性
97、你可以在 Spring 中注入一个 null 和一个空字符串吗？
98、什么是基于 Java 的 Spring 注解配置? 给一些注解的例子
99、什么是基于注解的容器配置?
100、怎样开启注解装配？
101、@Required 注解
102、@Autowired 注解
103、@Qualififier 注解
104、在 Spring 框架中如何更有效地使用 JDBC?
105、JdbcTemplate
106、Spring 对 DAO 的支持
107、使用 Spring 通过什么方式访问 Hibernate?
108、Spring 支持的 ORM
109、如何通过 HibernateDaoSupport 将 Spring 和 Hibernate结合起来？
110、Spring 支持的事务管理类型
111、Spring 框架的事务管理有哪些优点？
112、你更倾向用那种事务管理类型？
113、解释 AOP
114、Aspect 切面
115、在 Spring AOP 中，关注点和横切关注的区别是什么？
116、连接点
117、通知
118、切点
119、什么是引入?
120、什么是目标对象?
121、什么是代理?
122、有几种不同类型的自动代理？
123、什么是织入。什么是织入应用的不同点？
124、解释基于 XML Schema 方式的切面实现。
125、解释基于注解的切面实现
126、什么是 Spring 的 MVC 框架？
127、DispatcherServlet
128、WebApplicationContext
129、什么是 Spring MVC 框架的控制器？
130、@Controller 注解
131、@RequestMapping 注解


### Mybatis面试题

1、什么是 Mybatis？
2、Mybaits 的优点
3、MyBatis 框架的缺点
4、MyBatis 框架适用场合
5、MyBatis 与 Hibernate 有哪些不同？
6、#{}和${}的区别是什么？
7、当实体类中的属性名和表中的字段名不一样 ，怎么办 ？
8、 模糊查询 like 语句该怎么写?
9、通常一个 Xml 映射文件，都会写一个 Dao 接口与之对应，请问，这个 Dao 接口的工作
原理是什么？Dao 接口里的方法，参数不同时，方法能重载吗？
13、如何获取自动生成的(主)键值?
14、在 mapper 中如何传递多个参数?
15、Mybatis 动态 sql 有什么用？执行原理？有哪些动态 sql？
16、Xml 映射文件中，除了常见的 select|insert|updae|delete标签之外，还有哪些标签？
17、Mybatis 的 Xml 映射文件中，不同的 Xml 映射文件，id 是否可以重复？
18、为什么说 Mybatis 是半自动 ORM 映射工具？它与全自动的区别在哪里？
19、 一对一、一对多的关联查询 ？
20、MyBatis 实现一对一有几种方式?具体怎么操作的？
21、MyBatis 实现一对多有几种方式,怎么操作的？
22、Mybatis 是否支持延迟加载？如果支持，它的实现原理是什么？
23、Mybatis 的一级、二级缓存
24、什么是 MyBatis 的接口绑定？有哪些实现方式？
25、使用 MyBatis 的 mapper 接口调用时有哪些要求？
26、Mapper 编写有哪几种方式？
27、简述 Mybatis 的插件运行原理，以及如何编写一个插件。
28、MyBatis实现一对一有几种方式?具体怎么操作的 ？


### Springmvc面试题

1、什么是SpringMvc?
2、Spring MVC的优点？
3、SpringMVC工作原理?
4、SpringMVC流程？
5、SpringMVC的控制器是不是单例模式?如果是，有什么问题？怎么解决？
6、如果你也用过Struts2。简单介绍一下SpringMVC和Struts2的区别有哪些？
7、SpingMvc 中的控制器的注解一般用那个,有没有别的注解可以替代？
8、 @RequestMapping 注解用在类上面有什么作用？
9、怎么样把某个请求映射到特定的方法上面？
10、如果在拦截请求中,我想拦截 get 方式提交的方法,怎么配置？
11、怎么样在方法里面得到 Request,或者 Session？
12、我想在拦截的方法里面得到从前台传入的参数,怎么得到？
13、如果前台有很多个参数传入,并且这些参数都是一个对象的,那么怎么样快速得到这个对象？
14、SpringMvc 中函数的返回值是什么？
15、SpringMVC 怎么样设定重定向和转发的？
16、SpringMvc 用什么对象从后台向前台传递数据的？
17、SpringMvc 中有个类把视图和数据都合并的一起的,叫什么？
18、怎么样把 ModelMap 里面的数据放入 Session 里面？
19、SpringMVC怎么和Ajax相互调用的？
20、当一个方法向 AJAX 返回特殊对象,譬如 Object,List 等,需要做什么处理？
21、SpringMvc 里面拦截器是怎么写的？







一、ActiveMQ消息中间件篇

    什么是 ActiveMQ?
    ActiveMQ 服务器宕机怎么办？
    丢消息怎么办？
    持久化消息非常慢
    消息的不均匀消费
    死信队列
    ActiveMQ 中的消息重发时间间隔和重发次数吗？



二、MySQL篇（重要）

    一张表，里面有 ID 自增主键，当 insert 了 17 条记录之后，删除了第 15,16,17 条记录，再把 Mysql 重启，再 insert 一条记录，这条记录的 ID 是 18 还是 15 ？
    Mysql 的技术特点是什么？
    Heap 表是什么？
    Mysql 服务器默认端口是什么？
    如何区分 FLOAT 和 DOUBLE？
    区分 CHAR_LENGTH 和 LENGTH
    请简洁描述 Mysql 中 InnoDB 支持的四种事务隔离级别名称，以及逐级之间的区别
    在 Mysql 中 ENUM 的用法是什么？
    如何定义 REGEXP？
    CHAR 和 VARCHAR 的区别？
    列的字符串类型可以是什么？
    如何获取当前的 Mysql 版本？
    Mysql 中使用什么存储引擎？
    Mysql 驱动程序是什么？
    TIMESTAMP 在 UPDATE CURRENT_TIMESTAMP 数据类型上做什么？
    主键和候选键有什么区别？
    如何使用 Unix shell 登录 Mysql？
    myisamchk 是用来做什么的？
    MYSQL 数据库服务器性能分析的方法命令有哪些?
    如何做 mysql 的性能优化？

三、Dubbo篇

    Dubbo 支持哪些协议，每种协议的应用场景，优缺点？
    Dubbo 超时时间怎样设置？
    Dubbo 有些哪些注册中心？
    Dubbo 是什么？
    Dubbo 的主要应用场景？
    Dubbo 的核心功能？
    Dubbo 的核心组件？
    Dubbo 服务注册与发现的流程？
    Dubbo 的架构设计？
    Dubbo 的服务调用流程？
    Dubbo 中 zookeeper 做注册中心，如果注册中心集群都挂掉，发布者和订阅者之间还能通信么？
    Dubbo 服务负载均衡策略
    Dubbo 在安全机制方面是如何解决的？
    Dubbo 连接注册中心和直连的区别
    Dubbo 通信协议 dubbo 协议为什么采用异步单一长连接
    RMI 协议
    Hessian 协议

四、JVM篇（重要）

    说一下 jvm 的主要组成部分？及其作用？
    说一下 jvm 运行时数据区？
    说一下堆栈的区别？
    队列和栈是什么？有什么区别？
    什么是双亲委派模型？
    说一下类加载的执行过程？
    怎么判断对象是否可以被回收？
    java 中都有哪些引用类型？
    说一下 jvm 有哪些垃圾回收算法？
    说一下 jvm 有哪些垃圾回收器？
    详细介绍一下 CMS 垃圾回收器？
    新生代垃圾回收器和老生代垃圾回收器都有哪些？有什么区别？
    简述分代垃圾回收器是怎么工作的？
    说一下 jvm 调优的工具？
    常用的 jvm 调优的参数都有哪些？

五、Kafka篇

    kafka 可以脱离 zookeeper 单独使用吗？为什么？
    kafka 有几种数据保留的策略？
    kafka 同时设置了 7 天和 10G 清除数据，到第五天的时候消息达到了 10G，这个时候 kafka 将如何处理？
    什么情况会导致 kafka 运行变慢？
    使用 kafka 集群需要注意什么？
    Kafka 的设计是什么样的呢？
    Kafka 存储在硬盘上的消息格式是什么？
    Kafka 高效文件存储设计特点
    kafka 的 ack 机制

六、memcached篇

    memcached 是怎么工作的？
    memcached 最大的优势是什么？
    memcached 和 MySQL 的 query cache 相比，有什么优缺点？
    memcached 和服务器的 local cache（比如 PHP 的 APC、mmap 文件等）相比，有什么优点？
    memcached 的 cache 机制是怎样的？
    memcached 如何实现冗余机制？
    memcached 如何处理容错的？
    如何将 memcached 中 item 批量导入导出？
    我需要把 memcached 中的 item 批量导出导入，怎么办？
    memcached 是如何做身份验证的？
    memcached 的多线程是什么？如何使用它们？
    memcached 能接受的 key 的最大长度是多少？
    memcached 对 item 的过期时间有什么限制？
    为什么单个 item 的大小被限制在 1M byte 之内？


七、MongoDB篇

    你说的 NoSQL 数据库是什么意思?NoSQL 与 RDBMS 直接有什么区别?为什么要使用和不使用NoSQL 数据库?说一说 NoSQL 数据库的几个优点?
    NoSQL 数据库有哪些类型?
    MySQL 与 MongoDB 之间最基本的差别是什么?
    你怎么比较 MongoDB、CouchDB 及 CouchBase?
    MongoDB 成为最好 NoSQL 数据库的原因是什么?
    32 位系统上有什么细微差别?
    journal 回放在条目(entry)不完整时(比如恰巧有一个中途故障了)会遇到问题吗?
    分析器在 MongoDB 中的作用是什么?
    名字空间(namespace)是什么?
    如何执行事务/加锁?
    什么是 master 或 primary?
    数据在什么时候才会扩展到多个分片(shard)里


八、MyBatis篇（重要）

    mybatis 中 #{}和 ${}的区别是什么？
    mybatis 有几种分页方式？
    RowBounds 是一次性查询全部结果吗？为什么？
    mybatis 逻辑分页和物理分页的区别是什么？
    mybatis 是否支持延迟加载？延迟加载的原理是什么？
    说一下 mybatis 的一级缓存和二级缓存？
    mybatis 和 hibernate 的区别有哪些？
    mybatis 有哪些执行器（Executor）？
    mybatis 分页插件的实现原理是什么？
    mybatis 如何编写一个自定义插件？



九、Netty篇（重要）

    NIO 和 AIO 的区别？
    NIO 的组成？
    Netty 的特点？
    TCP 粘包/拆包的原因及解决方法？
    了解哪几种序列化协议？
    如何选择序列化协议？
    Netty 的零拷贝实现？
    Netty 的高性能表现在哪些方面？
    NIOEventLoopGroup 源码？


十、Nginx篇

    请解释一下什么是 Nginx?
    请列举 Nginx 的一些特性
    请列举 Nginx 和 Apache 之间的不同点
    请解释 Nginx 如何处理 HTTP 请求
    在 Nginx 中，如何使用未定义的服务器名称来阻止处理请求?
    使用“反向代理服务器”的优点是什么?
    请列举 Nginx 服务器的最佳用途
    请解释 Nginx 服务器上的 Master 和 Worker 进程分别是什么?
    请解释你如何通过不同于 80 的端口开启 Nginx?
    请解释是否有可能将 Nginx 的错误替换为 502 错误、503?
    在 Nginx 中，解释如何在 URL 中保留双斜线
    请解释 ngx_http_upstream_module 的作用是什么?
    请解释什么是 C10K 问题?
    请陈述 stub_status 和 sub_filter 指令的作用是什么?
    解释 Nginx 是否支持将请求压缩到上游?
    解释如何在 Nginx 中获得当前的时间?


十一、RabbitMQ篇

    rabbitmq 的使用场景有哪些？
    rabbitmq 有哪些重要的角色？
    rabbitmq 有哪些重要的组件？
    rabbitmq 中 vhost 的作用是什么？
    rabbitmq 的消息是怎么发送的？
    rabbitmq 怎么保证消息的稳定性？
    rabbitmq 怎么避免消息丢失？
    要保证消息持久化成功的条件有哪些？
    rabbitmq 持久化有什么缺点？
    rabbitmq 有几种广播类型？
    rabbitmq 怎么实现延迟消息队列？
    rabbitmq 集群有什么用？
    rabbitmq 节点的类型有哪些？
    rabbitmq 每个节点是其他节点的完整拷贝吗？为什么？
    rabbitmq 集群中唯一一个磁盘节点崩溃了会发生什么情况？
    rabbitmq 对集群节点停止顺序有要求吗？
    rabbitmq 集群搭建需要注意哪些问题？



十二、Redis篇（重要）

    redis 是什么？都有哪些使用场景？
    redis 有哪些功能？
    redis 和 memecache 有什么区别？
    redis 为什么是单线程的？
    什么是缓存穿透？怎么解决？
    redis 支持的数据类型有哪些？
    redis 和 redisson 有哪些区别？
    怎么保证缓存和数据库数据的一致性？
    redis 持久化有几种方式？
    redis 怎么实现分布式锁？
    redis 分布式锁有什么缺陷？
    redis 如何做内存优化？
    redis 淘汰策略有哪些？
    redis 常见的性能问题有哪些？该如何解决？


十三、Spring Cloud/Boot篇

    什么是 spring boot？
    为什么要用 spring boot？
    spring boot 核心配置文件是什么？
    spring boot 配置文件有哪几种类型？它们有什么区别？
    spring boot 有哪些方式可以实现热部署？
    jpa 和 hibernate 有什么区别？
    什么是 spring cloud？
    spring cloud 断路器的作用是什么？
    spring cloud 的核心组件有哪些？

十四、Spring/Spring MVC篇

    为什么要使用 spring？
    解释一下什么是 aop？
    解释一下什么是 ioc？
    spring 有哪些主要模块？
    spring 常用的注入方式有哪些？
    spring 中的 bean 是线程安全的吗？
    96.spring 支持几种 bean 的作用域？
    spring 自动装配 bean 有哪些方式？
    spring 事务实现方式有哪些？
    说一下 spring 的事务隔离？
    spring mvc 有哪些组件？
    @RequestMapping 的作用是什么？
    @Autowired 的作用是什么？



十五、SQL优化篇

    一张表，里面有 ID 自增主键，当 insert 了 17 条记录之后，删除了第 15,16,17 条记录，再把 Mysql 重启，再 insert 一条记录，这条记录的 ID 是 18 还是 15 ？
    Mysql 的技术特点是什么？
    Heap 表是什么？
    Mysql 服务器默认端口是什么？
    与 Oracle 相比，Mysql 有什么优势？
    如何区分 FLOAT 和 DOUBLE？
    区分 CHAR_LENGTH 和 LENGTH？
    请简洁描述 Mysql 中 InnoDB 支持的四种事务隔离级别名称，以及逐级之间的区别？
    在 Mysql 中 ENUM 的用法是什么
    如何定义 REGEXP？
    CHAR 和 VARCHAR 的区别？
    列的字符串类型可以是什么？


十六、Tomcat篇

    Tomcat 的缺省端口是多少，怎么修改？
    Tomcat 有哪几种 Connector 运行模式(优化)？
    Tomcat 有几种部署方式？
    Tomcat 容器是如何创建 servlet 类实例？用到了什么原理？
    Tomcat 如何优化？
    内存调优
    垃圾回收策略调优
    共享 session 处理
    添加 JMS 远程监控
    关于 Tomcat 的 session 数目
    监视 Tomcat 的内存使用情况
    打印类的加载情况及对象的回收情况
    Tomcat 一个请求的完整过程
    Tomcat 工作模式



十七、zookeeper篇

    ZooKeeper 是什么？
    ZooKeeper 提供了什么？
    Zookeeper 文件系统
    四种类型的 znode
    Zookeeper 通知机制
    Zookeeper 做了什么？
    zk 的命名服务（文件系统）
    zk 的配置管理（文件系统、通知机制）
    Zookeeper 集群管理（文件系统、通知机制）
    Zookeeper 分布式锁（文件系统、通知机制）



十八、并发编程篇

    Synchronized用过吗，其原理是什么 ？
    你刚才提到获取对象的锁，这个“锁”是什么？如何确定对象的锁？
    什么是可重入性？为什么说Synchronized是可重入锁？
    JVM对Java的原生锁做了哪些优化？
    为什么说Synchronized是非公平锁？
    什么是锁消除和锁粗化？
    为什么说Synchronized是一个悲观锁？乐观锁的实现原理又是什么？
    什么是CAS，它有什么特性？
    乐观锁一定就是好的吗？
    跟Synchronized相比，可重入ReentrantLock其实现原理有什么不同？
    请谈谈AQS框架是怎么回事
    请尽可能详尽地对比下Synchronized和ReentrantLock的异同
    ReentrantLock是如何实现可重入性的？
    除了ReentrantLock，你还接触过JUC中的哪些并发工具？
    请谈谈ReadWriteLock和StampedLock
    如何让Java的线程彼此同步？你还了解过哪些同步器？请分别介绍一下
    CyclicBarrier和CountDownLatch看起来很相似，请对比一下
    Java中的线程池是如何实现的？
    创建线程池的几个核心构造参数
    线程池中的线程是怎么创建的？是一开始就随着线程池的启动创建好的吗？
    既然提到可以通过配置不同参数创建不同的线程池，那么Java中默认实现好的线程池又有哪些？请比较它们的异同
    如何在Java线程池中提交线程？
    什么是Java的内存模型，Java中各个线程是怎么彼此看到对方的变量的？
    请谈谈Volatile有什么特点，它为什么能保证变量对所有线程的可见性？
    既然Volatile能保证县城见的变量可见性，是不是就意味着基于Volatile变量的运算就是并发安全的？
    请对比下Volatile和Synchronized的异同
    请谈谈RhreadLocal是怎么解决并发安全的？
    很多人都说要慎用TheadLocal，谈谈你的理解，使用TheadLocal需要注意些什么？



十九、多线程篇

    现在有 T1、T2、T3 三个线程，你怎样保证 T2 在 T1 执行完后执行，T3 在 T2 执行完后执行？
    用 Java 写代码来解决生产者——消费者问题
    用 Java 编程一个会导致死锁的程序，你将怎么解决？
    什么是原子操作，Java 中的原子操作是什么？
    Java 中的 volatile 关键是什么作用？怎样使用它？在 Java 中它跟 synchronized 方法有什么不同？
    你将如何使用 threaddump？你将如何分析 Thread dump？
    为什么我们调用 start()方法时会执行 run()方法，为什么我们不能直接调用 run()方法？
    Java 教你怎样唤醒一个阻塞的线程？
    在 Java 中 CycliBarriar 和 CountdownLatch 有什么区别？
    你在多线程环境中遇到的常见的问题是什么？你是怎么解决它的？



二十、开源框架篇

    BeanFactory 和 ApplicationContext 有什么区别？
    Spring Bean 的生命周期
    Spring IOC 如何实现？
    说说 Spring AOP
    Spring AOP 实现原理
    动态代理（cglib 与 JDK）
    Spring 事务实现方式
    Spring 事务底层原理
    如何自定义注解实现功能
    Spring MVC 运行流程
    Spring MVC 启动流程
    Spring 的单例实现原理
    Spring 框架中用到了哪些设计模式
    为什么选择 Netty
    说说业务中，Netty 的使用场景
    原生的 NIO 在 JDK 1.7 版本存在 epoll bug
    什么是 TCP 粘包/拆包
    TCP 粘包/拆包的解决办法
    Netty 线程模型
    说说 Netty 的零拷贝
    Netty 内部执行流程



二十一、设计模式篇

    请列举出在 JDK 中几个常用的设计模式？
    什么是设计模式？你是否在你的代码里面使用过任何设计模式？
    Java 中什么叫单例设计模式？请用 Java 写出线程安全的单例模式
    使用工厂模式最主要的好处是什么？在哪里使用？
    举一个用 Java 实现的装饰模式(decorator design pattern)？它是作用于对象层次还是类层次？
    在 Java 中，为什么不允许从静态方法中访问非静态变量？
    设计一个 ATM 机，请说出你的设计思路？
    在 Java 中，什么时候用重载，什么时候用重写？
    举例说明什么情况下会更倾向于使用抽象类而不是接口？



二十二、微服务篇

    前后端分离是如何做的
    微服务哪些框架
    说说 RPC 的实现原理
    说说 Dubbo 的实现原理



部分常见面试真题篇

    tomcat的配置，tomcat从配置到启动的细节过程，tomcat优化
    hashmap介绍一下
    concurrentHashmap、线程池，多线程的开启方式
    jvm内存结构
    jvm垃圾回收算法
    mysql存储引擎，区别
    mysql索引结构，事务、隔离级别，隔离级别每一级会出现的问题
    线程和进程区别，进程间的通信方式
    linux基本命令，如何查看端口是否开通，端口监听命令，抓取文件关键字命令等
    TCP和UDP区别
    三次握手
    介绍下Docker，什么场景使用
    Http和Https的区别
    Https怎么实现安全的加密传输
    Tcp三次握手和四次挥手的过程
    什么是僵尸进程
    什么是孤儿进程
    linux下常用的信号
    linux系统调用函数
    共享内存是什么
    tcp与udp的区别
    流量控制解决什么问题？采用什么算法
    拥塞控制解决什么问题，采用什么算法
    关闭连接的四次挥手
    操作系统一个栈一般多大
    讲讲快排原理，特点
    常用排序算法
    红黑树了解吗
    红黑树比平衡二叉树的优点在哪里，为什么
    数据库常用的索引是什么
    hash算法了解吗？用到哪里
    redis锁怎么实现
    为什么不用乐观锁，而是用redis
    redis为什么性能更高
    redis的基本数据类型
    redis的底层数据结构
