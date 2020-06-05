# 基于 Spring Cloud 完整的微服务架构实战

[![img](https://upload.jianshu.io/users/upload_avatars/13638982/22c4c181-49bf-48e7-bbcf-608d5cad9541.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96)](https://www.jianshu.com/u/4a35811f38e1)

[慕容千语](https://www.jianshu.com/u/4a35811f38e1)[![  ](https://upload.jianshu.io/user_badge/ec7b4a53-cd02-46ad-b136-dfa3751cff1e)](https://www.jianshu.com/mobile/campaign/day_by_day/join)

52020.04.09 13:09:07字数 2,683阅读 1,620

![img](https://upload-images.jianshu.io/upload_images/13638982-a805948a275428a4.png?imageMogr2/auto-orient/strip|imageView2/2/w/900)

**欢迎关注专栏：[Java架构技术进阶](https://www.jianshu.com/c/8d050bf89c61)。里面有大量batj面试题集锦，还有各种技术分享，如有好文章也欢迎投稿哦。**

# 前言

本文介绍了技术栈，应用架构，体系架构，应用组件，怎么启动项目，以及相关的项目预览，介绍较为详细，详情请看下文。

# 一、技术栈

- **Spring boot** - 微服务的入门级微框架，用来简化 Spring 应用的初始搭建以及开发过程。
- **Eureka** - 云端服务发现，一个基于 REST 的服务，用于定位服务，以实现云端中间层服务发现和故障转移。
- **Spring Cloud Config** - 配置管理工具包，让你可以把配置放到远程服务器，集中化管理集群配置，目前支持本地存储、Git 以及 Subversion。
- **Hystrix** - 熔断器，容错管理工具，旨在通过熔断机制控制服务和第三方库的节点,从而对延迟和故障提供更强大的容错能力。
- **Zuul - Zuul** 是在云平台上提供动态路由，监控，弹性，安全等边缘服务的框架。Zuul 相当于是设备和 Netflix 流应用的 Web 网站后端所有请求的前门。
- **Spring Cloud Bus** - 事件、消息总线，用于在集群（例如，配置变化事件）中传播状态变化，可与 Spring Cloud Config 联合实现热部署。
- **Spring Cloud Sleuth** - 日志收集工具包，封装了 Dapper 和 log-based 追踪以及 Zipkin 和 HTrace 操作，为 SpringCloud 应用实现了一种分布式追踪解决方案。
- **Ribbon** - 提供云端负载均衡，有多种负载均衡策略可供选择，可配合服务发现和断路器使用。
- **Turbine** - Turbine 是聚合服务器发送事件流数据的一个工具，用来监控集群下 hystrix 的 metrics 情况。
- **Spring Cloud Stream** - Spring 数据流操作开发包，封装了与 Redis、Rabbit、Kafka 等发送接收消息。
- **Feign - Feign** 是一种声明式、模板化的 HTTP 客户端。
- **Spring Cloud OAuth2** - 基于 Spring Security 和 OAuth2 的安全工具包，为你的应用程序添加安全控制。

# 二、应用架构

该项目包含 8 个服务

- **registry** - 服务注册与发现
- **config** - 外部配置
- **monitor** - 监控
- **zipkin** - 分布式跟踪
- **gateway** - 代理所有微服务的接口网关
- **auth-service** - OAuth2 认证服务
- **svca-service** - 业务服务A
- **svcb-service** - 业务服务B

**1. 体系架构**

![img](https://upload-images.jianshu.io/upload_images/20352904-b05b2b09d75fca64.png?imageMogr2/auto-orient/strip|imageView2/2/w/819)

**2. 应用组件**

![img](https://upload-images.jianshu.io/upload_images/20352904-396d877df00d877d.png?imageMogr2/auto-orient/strip|imageView2/2/w/805)

启动项目

使用 Docker 快速启动

1. 配置 Docker 环境
2. mvn clean package 打包项目及 Docker 镜像
3. 在项目根目录下执行 docker-compose up -d 启动所有项目

本地手动启动

1. 配置 rabbitmq
2. 修改 hosts 将主机名指向到本地，127.0.0.1 registry config monitor rabbitmq auth-service，或者修改各服务配置文件中的相应主机名为本地 ip
3. 启动 registry、config、monitor、zipkin
4. 启动 gateway、auth-service、svca-service、svcb-service

# 三、项目预览

**1. 注册中心**

访问`http://localhost:8761/`默认账号 user，密码 password

![img](https://upload-images.jianshu.io/upload_images/20352904-f9e89b582c558161.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

监控

访问`http://localhost:8040/`默认账号 admin，密码 admin

**2. 控制面板**

![img](https://upload-images.jianshu.io/upload_images/20352904-3e8762f70d039961.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**3. 应用注册历史**

![img](https://upload-images.jianshu.io/upload_images/20352904-ac9c68493943f901.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**4. Turbine Hystrix面板**

![img](https://upload-images.jianshu.io/upload_images/20352904-a5e2090141599c27.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**5. 应用信息、健康状况、垃圾回收等详情**

![img](https://upload-images.jianshu.io/upload_images/20352904-21e3f2b0dddaf057.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**6. 计数器**

![img](https://upload-images.jianshu.io/upload_images/20352904-bae4b5e862af9f6c.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**7. 查看和修改环境变量**

![img](https://upload-images.jianshu.io/upload_images/20352904-19f6ec2b5458c3df.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**8. 管理 Logback 日志级别**

![img](https://upload-images.jianshu.io/upload_images/20352904-2f9f4930be278595.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**9. 查看并使用 JMX**

![img](https://upload-images.jianshu.io/upload_images/20352904-d3f92c6adad04049.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**10. 查看线程**

![img](https://upload-images.jianshu.io/upload_images/20352904-0447e3b06f57026e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**11. 认证历史**

![img](https://upload-images.jianshu.io/upload_images/20352904-2d3068222313b81f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**12. 查看 Http 请求轨迹**

![img](https://upload-images.jianshu.io/upload_images/20352904-a06cae45352054c4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**13. Hystrix 面板**

![img](https://upload-images.jianshu.io/upload_images/20352904-901c67944fddb51f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**14. 链路跟踪**

访问`http://localhost:9411/`默认账号 admin，密码 admin

**15. 控制面板**

![img](https://upload-images.jianshu.io/upload_images/20352904-ee99c889b9513ae2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**16. 链路跟踪明细**

![img](https://upload-images.jianshu.io/upload_images/20352904-f33e80018c9b901d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**17. 服务依赖关系**

![img](https://upload-images.jianshu.io/upload_images/20352904-523f598fabed4879.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**18. RabbitMQ 监控**

Docker 启动访问 [http://localhost:15673/](https://links.jianshu.com/go?to=http%3A%2F%2Flocalhost%3A15673%2F) 默认账号 guest，密码 guest（本地 rabbit 管理系统默认端口15672）

![img](https://upload-images.jianshu.io/upload_images/20352904-d90f816a6d3d65c0.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

**19. 接口测试**

获取 Token

```ruby
curl -X POST -vu client:secret http://localhost:8060/uaa/oauth/token -H "Accept: application/json" -d "password=password&username=anil&grant_type=password&scope=read%20write"
```

返回如下格式数据：

```json
{
    "access_token": "eac56504-c4f0-4706-b72e-3dc3acdf45e9",
    "token_type": "bearer",
    "refresh_token": "da1007dc-683c-4309-965d-370b15aa4aeb",
    "expires_in": 3599,
    "scope": "read write"
}
```

使用 access token 访问 service a 接口

```cpp
curl -i -H "Authorization: Bearer eac56504-c4f0-4706-b72e-3dc3acdf45e9" http://localhost:8060/svca
```

返回如下数据：

```dart
svca-service (172.18.0.8:8080)===>name:zhangxd
svcb-service (172.18.0.2:8070)===>Say Hello
```

使用 access token 访问 service b 接口

```cpp
curl -i -H "Authorization: Bearer eac56504-c4f0-4706-b72e-3dc3acdf45e9" http://localhost:8060/svcb
```

返回如下数据：

```dart
svcb-service (172.18.0.2:8070)===>Say Hello
```

使用 refresh token 刷新 token

```ruby
curl -X POST -vu client:secret http://localhost:8060/uaa/oauth/token -H "Accept: application/json" -d "grant_type=refresh_token&refresh_token=da1007dc-683c-4309-965d-370b15aa4aeb"
```

返回更新后的 Token：

```json
{
    "access_token": "63ff57ce-f140-482e-ba7e-b6f29df35c88",
    "token_type": "bearer",
    "refresh_token": "da1007dc-683c-4309-965d-370b15aa4aeb",
    "expires_in": 3599,
    "scope": "read write"
}
```

刷新配置

```cpp
curl -X POST -vu user:password http://localhost:8888/bus/refresh
```

**最近整理了一套微服务实战文档，讲解很透彻。今天分享给大家。这份资料尤其适合以下人群：**

> 1.没有用过微服务技术，只会用传统的 SSM 框架
>
> 2.用过 Spring Cloud、Dubbo等技术，但是只限于使用，遇到问题基本无法解决
>
> 3.从来没有系统学习微服务架构，觉得架构设计是遥不可及的
>
> 4.对于微服务技术有所了解，但尚没有设计高可用高并发的实践经历

**看完这份文档你将获得哪些收获？**

阐述微服务架构落地的一些设计原则和利弊取舍，结合微服务架构过程的很多最佳实践经验，希望给读者带来一定的启发和思考，避免在实际应用过程中走弯路，能够多快好省的落地实现微服务架构。

> **由于篇幅限制，小编这里只将此实战文档的所含内容全部展现出来了，需要获取完整文档用以学习的朋友们可以关注一下小编，点击[腾讯文档](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.qq.com%2Fdoc%2FDY2xNZ2dvcmNpWExj)获取免费领取方式！**

**文档内容目录**

1. 基础知识
2. 微服务构建（Spring Boot）
3. 服务治理（Spring Cloud Eureka）
4. 客户端负载均衡（Spring Cloud Ribbon）
5. 服务容错保护（Spring Cloud Hystrix）
6. 声明式服务调用（Spring Cloud Feign）
7. API网关服务（Spring Cloud Zuul）
8. 分布式配置中心（Spring Cloud Config）
9. 消息总线（Spring Cloud Bus）
10. 消息驱动的微服务（Spring Cloud Stream）
11. 分布式服务追踪（Spring Cloud Sleuth）

**基础知识**

主要包括了什么是微服务架构、与单体系统的区别、为什么选择Spring Cloud、什么是Spring Cloud

![img](https://upload-images.jianshu.io/upload_images/13638982-157123c1fdb8c2a1?imageMogr2/auto-orient/strip|imageView2/2/w/560)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**微服务构建（Spring Boot）**

**主要包含了：**框架简介、快速入门、项目构建与解析、实现RESTfulAPI、配置详解、自定义参数、参数引用、命令行参数、多环境配置、加载顺序、监控与管理、初识actuator、原生端点。

![img](https://upload-images.jianshu.io/upload_images/13638982-99f7daf88bda19ff?imageMogr2/auto-orient/strip|imageView2/2/w/572)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**服务治理（Spring Cloud Eureka）**

**主要内容包括：**服务治理、Netflix Eureka、注册服务提供者、高可用注册中心、服务发现与消费、Eureka详解、服务治理机制、源码分析、配置详解、服务注册类配置、服务实例类配置、跨平台支持。

![img](https://upload-images.jianshu.io/upload_images/13638982-983f637494c8573a?imageMogr2/auto-orient/strip|imageView2/2/w/555)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**客户端负载均衡（Spring Cloud Ribbon）**

**主要内容包括：**客户端负载均衡、RestTemplate 详解、GET请求、POST请求、PUT请求、DELETE请求、源码分析、负载均衡器、负载均衡策略、配置详解、自动化配置、Camden版本对RibbonClient配置的优化、参数配置、与Eureka结合、重试机制。

![img](https://upload-images.jianshu.io/upload_images/13638982-ae137ebb63d2f010?imageMogr2/auto-orient/strip|imageView2/2/w/550)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**服务容错保护（Spring Cloud Hystrix）**

**主要内容包括：**快速入门、原理分析、工作流程、断路器原理、依赖隔离、使用详解、创建请求命令、定义服务降级、异常处理、命令名称、 分组以及线程池划分、请求缓存、请求合并、属性详解、Command属性、collapser属性、thread  Pool属性、Hystrix仪表盘、Turbine集群监控、构建监控聚合服务、与消息代理结合。

![img](https://upload-images.jianshu.io/upload_images/13638982-bd3260bba6db386a?imageMogr2/auto-orient/strip|imageView2/2/w/561)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**声明式服务调用：**快速入门、继承特性、参数绑定、Ribbon配置、全局配置、指定服务配置、重试机制、Hystrix配置、全局配置、禁用Hystrix、指定命令配置、服务降级配置、其他配置、日志配置。

![img](https://upload-images.jianshu.io/upload_images/13638982-09e1ee709d065c0e?imageMogr2/auto-orient/strip|imageView2/2/w/581)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**API网关服务（Spring Cloud Zuul）**

快速入门、构建网关、请求路由、请求过滤、路由详解、传统路由配置、服务路由配置、服务路由的默认规则、自定义路由映射规则、路径匹配、路由前缀、本地跳转、Cookie与头信息、Hystrix 和 Ribbon 支持、过滤器详解、过滤器、请求生命周期、核心过滤器、异常处理、禁用过滤器、动态加载、动态路由、动态过滤器。

![img](https://upload-images.jianshu.io/upload_images/13638982-690a13b15a8ec500?imageMogr2/auto-orient/strip|imageView2/2/w/576)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**分布式配置中心：**快速入门、构建配置中心、配置规则详解、客户端配置映射、服务端详解、基础架构、Git配置仓库、SVN配置仓库、本地仓库、本地文件系统、健康监测、属性覆盖、安全保护、加密解密、高可用配置、客户端详解、服务化配置中心、失败快速响应与重试、获取远程配置、动态刷新配置。

![img](https://upload-images.jianshu.io/upload_images/13638982-4e546307b8308371?imageMogr2/auto-orient/strip|imageView2/2/w/564)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**消息总线：**消息代理、RabbitMQ实现消息总线、基本概念、安装与使用、快速入门、整合Spring  Cloud Bus、原理分析、指定刷新范围、架构优化、RabbitMQ配置、Kafka实现消息总线、Kafka简介、快速入门、整合 Spring Cloud Bus、Kafka配置、深入理解、源码分析、其他消息代理的支持。

![img](https://upload-images.jianshu.io/upload_images/13638982-25ecd0edf83c4878?imageMogr2/auto-orient/strip|imageView2/2/w/563)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**消息驱动的微服务：**快速入门、核心概念、绑定器、发布－订阅模式、消费组、消息分区、使用详解、开启绑定功能、绑定消息通道、消息生产与消费、响应式编程、消费组与消息分区、消息类型、绑定器详解、绑定器SPI、自动化配置、多绑定器配置、RabbitMQ与Kafka绑定器、配置详解、基础配置、绑定通道配置、绑定器配置。

![img](https://upload-images.jianshu.io/upload_images/13638982-a55d30e863088ea1?imageMogr2/auto-orient/strip|imageView2/2/w/564)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**分布式服务跟踪：**快速入门、准备工作、实现跟踪、跟踪原理、抽样收集、与Logstash整合、与Zipkin整合、HTTP收集、消息中间件收集、收集原理、数据存储、API接口。

![img](https://upload-images.jianshu.io/upload_images/13638982-0f01e49638acc738?imageMogr2/auto-orient/strip|imageView2/2/w/546)

终于有人把微服务架构讲清了！这估计是史上最全的一篇微服务实战

**由于篇幅限制，小编这里只将此实战文档的所含内容全部展现出来了，需要获取完整文档用以学习的朋友们可以关注一下小编，点击[腾讯文档](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.qq.com%2Fdoc%2FDY2xNZ2dvcmNpWExj)获取免费领取方式！**