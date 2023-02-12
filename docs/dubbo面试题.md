### 1、说一下dubbo的调用过程

### 2、dubbo的工作原理

![img](https://img-blog.csdnimg.cn/img_convert/f86068628ff3d56903cab03299f09186.png)

1、服务容器负责启动，加载，运行服务提供者。
2、服务提供者在启动时，向注册中心注册自己提供的服务。
3、服务消费者在启动时，向注册中心订阅自己所需的服务。
4、注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者。
5、服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。
6、服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心。

### 3，Dubbo支持哪些协议？

**dubbo**：单一长连接和 NIO 异步通讯，适合大并发小数据量的服务调用，以及消费者远大于提供者。传输协议 TCP，异步，Hessian 序列化；

**rmi**：采用 JDK 标准的 rmi 协议实现，传输参数和返回参数对象需要实现 Serializable 接口，使用 java 标准序列化机制，使用阻塞式短连接，传输数据包大小混合，消费者和提供者个数差不多，可传文件，传输协议 TCP。 多个短连接，TCP 协议传输，同步传输，适用常规的远程服务调用和 rmi 互操作。在依赖低版本的 Common-Collections 包，java 序列化存在安全漏洞；

**webservice**：基于 WebService 的远程调用协议，集成 CXF 实现，提供和原生 WebService 的互操作。多个短连接，基于 HTTP 传输，同步传输，适用系统集成和跨语言调用；http： 基于 Http 表单提交的远程调用协议，使用 Spring 的 HttpInvoke 实现。多个短连接，传输协议 HTTP，传入参数大小混合，提供者个数多于消费者，需要给应用程序和浏览器 JS 调用； hessian： 集成 Hessian 服务，基于 HTTP 通讯，采用 Servlet 暴露服务，Dubbo 内嵌 Jetty 作为服务器时默认实现，提供与 Hession 服务互操作。多个短连接，同步 HTTP 传输，Hessian 序列化，传入参数较大，提供者大于消费者，提供者压力较大，可传文件；

**memcache**： 基于 Memcached 实现的 RPC 协议 Redis： 基于 Redis 实现的 RPC 协议


### 4，注册中心挂了，consumer还能不能调用provider？

可以的，启动 dubbo 时，消费者会从 zookeeper 拉取注册的生产者的地址接口等数据，缓存在本地。

每次调用时，按照本地存储的地址进行调用。provider才调用不通

### 5，怎么实现动态感知服务下线的呢？

服务订阅通常有 pull 和 push 两种方式：

pull 模式需要客户端定时向注册中心拉取配置；

push 模式采用注册中心主动推送数据给客户端；

DubboZookeeper注册中心采用是事件通知与客户端拉取方式。服务第一次订阅的时候将会拉取对应目录下全量数据，然后在订阅的节点注册一个 watcher。一旦目录节点下发生任何数据变化，Zookeeper将会通过 watcher 通知客户端。客户端接到通知，将会重新拉取该目录下全量数据，并重新注册 watcher。利用这个模式，Dubbo服务就可以就做到服务的动态发现。

注意：Zookeeper提供了“心跳检测”功能，它会定时向各个服务提供者发送一个请求（实际上建立的是一个 socket 长连接），如果长期没有响应，服务中心就认为该服务提供者已经“挂了”，并将其剔除。

### 6，说说Dubbo与Spring Cloud的区别？

**通信方式**：Dubbo使用的是RPC通信，Spring Cloud使用的是HTTP RestFul方式

**注册中心**：Dubbo使用Zookeeper（官方推荐），还有Redis、Multicast、Simple注册中心，但不推荐，

Spring Cloud使用的是Spring Cloud Netflix Eureka

**监控**：Dubbo使用的是Dubbo-monitor，Spring Cloud使用的是Spring Boot admin

**断路器**：Dubbo在断路器这方面还不完善，Spring Cloud使用的是Spring Cloud Netflix Hystrix

分布式配置、网关服务、服务跟踪、消息总线、批量任务等

### 7、dubbo负载均衡怎么实现？

客户端使用MockClusterInvoker对象调用远程服务。默认情况下，MockClusterInvoker对象将调用远程服务的任务委托给FailoverClusterInvoker。FailoverClusterInvoker通过select方法选择合适的服务。select方法的入参包括负载均衡对象，InvokerWrapper对象集合等，其中每个服务对应一个InvokerWrapper对象，InvokerWrapper对象是对远程调用服务的包装类。


### 8、dobbo泛化调用过程原理？




### 9、dubbo超时时间怎么设置？

dubbo服务超时时间有xml和注解两种方式进行实现配置超时功能。在配置范围上分为全部超时配置、接口类上超时配置、以及接口方法上超时配置。同类型上的配置消费端优先提供着端，靠近原则方法配置优先于接口类全局配置优先级最低。所以dubbo的超时时间优先级为：**消费者Method>提供者method>消费者Reference>提供者Service>消费者全局配置provider>提供者全局配置consumer**。

### 10、服务调用是阻塞的吗？

默认是阻塞的，可以异步调用，没有返回值的可以这么做。

### 11、dubbo安全机制方面如何解决？

dubbo 通过 token 令牌防止用户绕过注册中心直连，然后在注册中心管理授权，dubbo 提供了黑白名单，控制服务所允许的调用方。

### 12、Dubbo SPI 和 Java SPI 区别？

JDK 标准的 SPI 会一次性加载所有的扩展实现，如果有的扩展很耗时，但也没用上，很浪费资源。所以只希望加载某个的实现，就不现实了

DUBBO SPI：

1、 对 Dubbo 进行扩展，不需要改动 Dubbo 的源码

2、 延迟加载，可以一次只加载自己想要加载的扩展实现。

3、 增加了对扩展点 IOC 和 AOP 的支持，一个扩展点可以直接 setter 注入其它扩展点。

4、 Dubbo 的扩展机制能很好的支持第三方 IoC 容器，默认支持 Spring Bean。

### 13、Dubbo 的整体架构设计有哪些分层?

**接口服务层（Service）**：该层与业务逻辑相关，根据 provider 和 consumer 的业务设计对应的接口和实现

**配置层（Config）**：对外配置接口，以 ServiceConfig 和 ReferenceConfig 为中心

**服务代理层（Proxy）**：服务接口透明代理，生成服务的客户端 Stub 和 服务端的 Skeleton，以 ServiceProxy 为中心，扩展接口为 ProxyFactory

**服务注册层（Registry**）：封装服务地址的注册和发现，以服务 URL 为中心，扩展接口为 RegistryFactory、Registry、RegistryService

**路由层（Cluster）**：封装多个提供者的路由和负载均衡，并桥接注册中心，以Invoker 为中心，扩展接口为 Cluster、Directory、Router和LoadBlancce

**监控层（Monitor）**：RPC调用次数和调用时间监控，以 Statistics 为中心，扩展接口为 MonitorFactory、Monitor和MonitorService

**远程调用层（Protocal）**：封装 RPC 调用，以 Invocation 和 Result 为中心，扩展接口为 Protocal、Invoker和Exporter

**信息交换层（Exchange）**：封装请求响应模式，同步转异步。以 Request 和 Response 为中心，扩展接口为 Exchanger、ExchangeChannel、ExchangeClient和ExchangeServer

**网络传输层（Transport）**：抽象 mina 和 netty 为统一接口，以 Message 为中心，扩展接口为Channel、Transporter、Client、Server和Codec

**数据序列化层（Serialize）**：可复用的一些工具，扩展接口为Serialization、 ObjectInput、ObjectOutput和ThreadPool

### 14、Dubbo 的使用场景有哪些？

1、 透明化的远程方法调用：就像调用本地方法一样调用远程方法，只需简单配置，没有任何API侵入。

2、 软负载均衡及容错机制：可在内网替代 F5 等硬件负载均衡器，降低成本，减少单点。

3、 服务自动注册与发现：不再需要写死服务提供方地址，注册中心基于接口名查询服务提供者的IP地址，并且能够平滑添加或删除服务提供者。

### 15、Dubbo服务降级，失败重试怎么做？

可以通过dubbo:reference 中设置mock="return null"。mock的值也可以修改为true，然后在跟接口同一个路径下实现一个Mock类，命名规则是"接口名称+Mock"后缀。然后在Mock类里实现自己的降级逻辑。

### 16、dubbo支持哪些系列化方式？

1. hessian2：跨语言的高效二进制序列化方式。但这里实际不是原生的hessian2序列化，而是阿里修改过的，它是dubbo RPC默认启用的序列化方式。

2. avro：将数据结构或对象转化成便于存储或传输的格式。Avro设计之初就用来支持数据密集型应用，适合于远程或本地大规模数据的存储和交换。


3. fastjson：一个Java语言编写的高性能功能完善的JSON库。它采用一种“假定有序快速匹配”的算法，把JSON Parse的性能提升到极致，是目前Java语言中最快的JSON库。Fastjson接口简单易用，已经被广泛使用在缓存序列化、协议交互、Web输出、Android客户端等多种应用场景。


4. fst：重新实现的 Java 快速对象序列化的开发包。序列化速度更快（2-10倍）、体积更小，而且兼容 JDK 原生的序列化。

5. gson：一个简单的基于Java的库，用于将Java对象序列化为JSON，反之亦然。 它是由Google开发的一个开源库。


6. jdk：JDK自带序列化。

7. kryo：一个快速高效的Java对象图形序列化框架，主要特点是性能、高效和易用。该项目用来序列化对象到文件、数据库或者网络。

8. protobuf： Google 的语言中立、平台中立、可扩展的结构化数据序列化机制。

9. protostuff：一个 java 序列化库，内置支持向前向后兼容性（模式演变）和验证。

来自：https://blog.csdn.net/qq_43437874/article/details/120178606


### 17、dubbo注册发现流程？

1、首先服务的提供者启动服务到注册中心注册，包括各种ip端口信息，Dubbo会同时注册该项目提供的远程调用的方法

2、服务的消费者(使用者)注册到注册中心，订阅发现

3、当有新的远程调用方法注册到注册中心时，注册中心会通知服务的消费者有哪些新的方法，如何调用

4、RPC调用：服务的调用者就无需知道ip和端口号，只需要服务名称就可以调用到服务提供者的方法
