

### 一、 什么是微服务架构

#### **1\. 什么是微服务架构**

微服务架构就是将单体的应用程序分成多个应用程序，这多个应用程序就成为微服务，每个微服务运行在自己的进程中，并使用轻量级的机制通信。这些服务围绕业务能力来划分，并通过自动化部署机制来独立部署。这些服务可以使用不同的编程语言，不同数据库，以保证最低限度的集中式管理。

#### **2\. 为什么需要学习Spring Cloud**

+   首先springcloud基于spingboot的优雅简洁，可还记得我们被无数xml支配的恐惧？可还记得 springmvc，mybatis错综复杂的配置，有了spingboot，这些东西都不需要了，spingboot好处不 再赘诉，springcloud就基于SpringBoot把市场上优秀的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理
+   什么叫做开箱即用？即使是当年的黄金搭档dubbo+zookeeper下载配置起来也是颇费心神的！而springcloud完成这些只需要一个jar的依赖就可以了！
+   springcloud大多数子模块都是直击痛点，像zuul解决的跨域，fegin解决的负载均衡，hystrix的熔断机制等等等等

#### **3\. Spring Cloud 是什么**

+   Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、智能路由、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。
+   Spring Cloud并没有重复制造轮子，它只是将各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。

#### **4\. SpringCloud的优缺点**

**优点：**

1.耦合度比较低。不会影响其他模块的开发。

2.减轻团队的成本，可以并行开发，不用关注其他人怎么开发，先关注自己的开发。

3.配置比较简单，基本用注解就能实现，不用使用过多的配置文件。

4.微服务跨平台的，可以用任何一种语言开发。

5.每个微服务可以有自己的独立的数据库也有用公共的数据库。

6.直接写后端的代码，不用关注前端怎么开发，直接写自己的后端代码即可，然后暴露接口，通过组件进行服务通信。

**缺点：**

1.部署比较麻烦，给运维工程师带来一定的麻烦。

2.针对数据的管理比麻烦，因为微服务可以每个微服务使用一个数据库。

3.系统集成测试比较麻烦

4.性能的监控比较麻烦。【最好开发一个大屏监控系统】

+   总的来说优点大过于缺点，目前看来Spring Cloud是一套非常完善的分布式框架，目前很多企业开始用微服务、Spring Cloud的优势是显而易见的。因此对于想研究微服务架构的同学来说，学习Spring Cloud是一个不错的选择。

#### **5\. SpringBoot和SpringCloud的区别？**

+   SpringBoot专注于快速方便的开发单个个体微服务。
+   SpringCloud是关注全局的微服务协调整理治理框架，它将SpringBoot开发的一个个单体微服务整合并管理起来，
+   为各个微服务之间提供，配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等集成服务
+   SpringBoot可以离开SpringCloud独立使用开发项目， 但是SpringCloud离不开SpringBoot ，属于依赖的关系
+   SpringBoot专注于快速、方便的开发单个微服务个体，SpringCloud关注全局的服务治理框架。

#### **6\. Spring Cloud和SpringBoot版本对应关系**

![](https://img-blog.csdnimg.cn/img_convert/8cdefd7de0c879a993693a18eb19a460.png)

#### **7\. SpringCloud由什么组成**

+   这就有很多了，我讲几个开发中最重要的
+   Spring Cloud Eureka：服务注册与发现
+   Spring Cloud Zuul：服务网关
+   Spring Cloud Ribbon：客户端负载均衡
+   Spring Cloud Feign：声明性的Web服务客户端
+   Spring Cloud Hystrix：断路器
+   Spring Cloud Confifig：分布式统一配置管理
+   等20几个框架，开源一直在更新

#### **8\. 使用 Spring Boot 开发分布式微服务时，我们面临什么问题**

+   （1）与分布式系统相关的复杂性-这种开销包括网络问题，延迟开销，带宽问题，安全问题。
+   （2）服务发现-服务发现工具管理群集中的流程和服务如何查找和互相交谈。它涉及一个服务目录，在该目录中注册服务，然后能够查找并连接到该目录中的服务。
+   （3）冗余-分布式系统中的冗余问题。
+   （4）负载平衡 --负载平衡改善跨多个计算资源的工作负荷，诸如计算机，计算机集群，网络链路，中央处理单元，或磁盘驱动器的分布。
+   （5）性能-问题 由于各种运营开销导致的性能问题。

#### **9\. Spring Cloud 和dubbo区别?**

+   （1）服务调用方式：dubbo是RPC springcloud Rest Api
+   （2）注册中心：dubbo 是zookeeper springcloud是eureka，也可以是zookeeper
+   （3）服务网关，dubbo本身没有实现，只能通过其他第三方技术整合，springcloud有Zuul路由网关，作为路由服务器，进行消费者的请求分发,springcloud支持断路器，与git完美集成配置文件支持版本控制，事物总线实现配置文件的更新与服务自动装配等等一系列的微服务架构要素。

### 二、Eureka

#### **10\. 服务注册和发现是什么意思？Spring Cloud 如何实现？**

![](https://img-blog.csdnimg.cn/img_convert/0db3dd9fe93d3101e94c6d7cbfd37848.png)

#### **11\. 什么是Eureka**

+   Eureka作为SpringCloud的服务注册功能服务器，他是服务注册中心，系统中的其他服务使用Eureka的客户端将其连接到Eureka Service中，并且保持心跳，这样工作人员可以通过EurekaService来监控各个微服务是否运行正常。

#### **12\. Eureka怎么实现高可用**

+   集群吧，注册多台Eureka，然后把SpringCloud服务互相注册，客户端从Eureka获取信息时，按照Eureka的顺序来访问。

#### **13\. 什么是Eureka的自我保护模式，**

+   默认情况下，如果Eureka Service在一定时间内没有接收到某个微服务的心跳，Eureka Service会进入自我保护模式，在该模式下Eureka Service会保护服务注册表中的信息，不在删除注册表中的数据，当网络故障恢复后，Eureka Servic 节点会自动退出自我保护模式

#### **14\. DiscoveryClient的作用**

+   可以从注册中心中根据服务别名获取注册的服务器信息。

#### **15\. Eureka和ZooKeeper都可以提供服务注册与发现的功能,请说说两个的区别**

1.  ZooKeeper中的节点服务挂了就要选举 在选举期间注册服务瘫痪,虽然服务最终会恢复,但是选举期间不可用的， 选举就是改微服务做了集群，必须有一台主其他的都是从
2.  Eureka各个节点是平等关系,服务器挂了没关系，只要有一台Eureka就可以保证服务可用，数据都是最新的。 如果查询到的数据并不是最新的，就是因为Eureka的自我保护模式导致的
3.  Eureka本质上是一个工程,而ZooKeeper只是一个进程
4.  Eureka可以很好的应对因网络故障导致部分节点失去联系的情况,而不会像ZooKeeper 一样使得整个注册系统瘫痪
5.  ZooKeeper保证的是CP，Eureka保证的是AP

CAP： C：一致性>Consistency; 取舍：(强一致性、单调一致性、会话一致性、最终一致性、弱一致性) A：可用性>Availability; P：分区容错性>Partition tolerance;

### 三、Zuul

#### **16\. 什么是网关?**

+   网关相当于一个网络服务架构的入口，所有网络请求必须通过网关转发到具体的服务。

#### **17\. 网关的作用是什么**

+   统一管理微服务请求，权限控制、负载均衡、路由转发、监控、安全控制黑名单和白名单等

#### **18\. 什么是Spring Cloud Zuul（服务网关）**

![](https://img-blog.csdnimg.cn/img_convert/7d2cc5ce3c67c3d2616b913995306114.png)

#### **19\. 网关与过滤器有什么区别**

+   网关是对所有服务的请求进行分析过滤，过滤器是对单个服务而言。

#### **20\. 常用网关框架有那些？**

+   Nginx、Zuul、Gateway

#### **21\. Zuul与Nginx有什么区别？**

+   Zuul是java语言实现的，主要为java服务提供网关服务，尤其在微服务架构中可以更加灵活的对网关进行操作。Nginx是使用C语言实现，性能高于Zuul，但是实现自定义操作需要熟悉lua语言，对程序员要求较高，可以使用Nginx做Zuul集群。

#### **22\. 既然Nginx可以实现网关？为什么还需要使用Zuul框架**

+   Zuul是SpringCloud集成的网关，使用Java语言编写，可以对SpringCloud架构提供更灵活的服务。

#### **23\. 如何设计一套API接口**

+   考虑到API接口的分类可以将API接口分为开发API接口和内网API接口，内网API接口用于局域网，为内部服务器提供服务。开放API接口用于对外部合作单位提供接口调用，需要遵循Oauth2.0权限认证协议。同时还需要考虑安全性、幂等性等问题。

#### **24\. ZuulFilter常用有那些方法**

+   Run()：过滤器的具体业务逻辑
+   shouldFilter()：判断过滤器是否有效
+   fifilterOrder()：过滤器执行顺序
+   fifilterType()：过滤器拦截位置

#### **25\. 如何实现动态Zuul网关路由转发**

+   通过path配置拦截请求，通过ServiceId到配置中心获取转发的服务列表，Zuul内部使用Ribbon实现本地负载均衡和转发。

#### **26\. Zuul网关如何搭建集群**

+   使用Nginx的upstream设置Zuul服务集群，通过location拦截请求并转发到upstream，默认使用轮询机制对Zuul集群发送请求。

### 四、Ribbon

#### **27\. 负载平衡的意义什么？**

![](https://img-blog.csdnimg.cn/img_convert/146958b09ae50a5df6e20748a57a6ee9.png)

#### **28\. Ribbon是什么？**

![](https://img-blog.csdnimg.cn/img_convert/9320df7bdda33fe712ad04b8a655fb5f.png)

#### **29\. Nginx与Ribbon的区别**

![](https://img-blog.csdnimg.cn/img_convert/43e1b9d608c5a0edca081611865a7ec5.png)

#### **30\. Ribbon底层实现原理**

+   Ribbon使用discoveryClient从注册中心读取目标服务信息，对同一接口请求进行计数，使用%取余算法获取目标服务集群索引，返回获取到的目标服务信息。

**@LoadBalanced注解的作用**

+   开启客户端负载均衡。

### 五、Hystrix

#### **31\. 什么是断路器**

![](https://img-blog.csdnimg.cn/img_convert/5cde4aeafd112af4f36ba1232b050139.png)

#### **32\. 什么是 Hystrix？**

![](https://img-blog.csdnimg.cn/img_convert/6ebd52cd6f2c8b58a5393774c0bb4af8.png)

#### **33\. 谈谈服务雪崩效应**

![](https://img-blog.csdnimg.cn/img_convert/a220fa89e3d96a749945f3e60b6932b4.png)

#### **34\. 在微服务中，如何保护服务?**

![](https://img-blog.csdnimg.cn/img_convert/87aa6fbacdbd2c5c28ac3e076d946cdc.png)

#### **35\. 服务雪崩效应产生的原因**

+   因为Tomcat默认情况下只有一个线程池来维护客户端发送的所有的请求，这时候某一接口在某一时刻被大量访问就会占据tomcat线程池中的所有线程，其他请求处于等待状态，无法连接到服务接口。

#### **36\. 谈谈服务降级、熔断、服务隔离**

![](https://img-blog.csdnimg.cn/img_convert/f3282575669b6a61e76172f6eaa83c18.png)

#### **37\. 服务降级底层是如何实现的？**

Hystrix实现服务降级的功能是通过重写HystrixCommand中的getFallback()方法，当Hystrix的run方法或construct执行发生错误时转而执行getFallback()方法。

### 六、Feign

#### **38\. 什么是Feign？**

#### **39\. SpringCloud有几种调用接口方式**

#### **40\. Ribbon和Feign调用服务的区别**

### 七、Bus

#### **41\. 什么是 Spring Cloud Bus？**

spring cloud是按照spring的配置对一系列微服务框架的集成，spring cloud bus是其中一个微服务框架，用于实现微服务之间的通信。
spring cloud bus整合 java的事件处理机制和消息中间件消息的发送和接受，主要由发送端、接收端和事件组成。针对不同的业务需求，可以设置不同的事件，发送端发送事件，接收端接受相应的事件，并进行相应的处理。
目前 Spring Cloud Bus 支持两种消息代理：RabbitMQ 和 Kafka
需要配合springcloud config使用


### 八、Config

**42\. 什么是Spring Cloud Config?**

**43\. 分布式配置中心有那些框架？**

**44\. 分布式配置中心的作用？**

**45\. SpringCloud Config 可以实现实时刷新吗？**

### 九、Gateway

#### **46\. 什么是Spring Cloud Gateway?**

Spring Cloud Gateway是Spring Cloud的一个全新的API网关项目，目的是为了替换掉Zuul1

- 路由转发：这是网关最主要的功能，通过配置统一将请求转发至相应的服务，否则客户端需多次请求不同的微服务，增加客户端代码或配置编写的复杂性，目前官网给出的配置条件有：After（某个时间后的请求转发至该服务）、Before（某个时间前的请求转发至该服务）、Between（某个时间范围的请求转发至该服务）、Cookie（匹配到对应的Cookie值）、Header（匹配到对应的Header值）、Host（匹配到对应的域名）、Method（匹配到对应的get/post请求）、Path（匹配到对应的url）、Query（匹配到对应的参数）、RemoteAddr（匹配到对应的RemoteAddr）、Weight（设定分流的权重）
- 熔断：在服务出现宕机时，网关会进行熔断，转发至熔断接口进行请求，通过配置FallbackHeaders GatewayFilter Factory从而引入Hystrix进行熔断
- 限流：当请求数过大时，我们需要对请求数进行限制，避免服务因此宕机，通过配置RequestRateLimiter GatewayFilter Factory对请求进行限流
- 鉴权：网关层可以对请求进行统一鉴权，比如客户的登录的登录状态，通过实现Global Filters可完成全局的鉴权，实现Gateway Filter可完成单个路由的鉴权



### 十、 SpringCloud主要项目

#### **47\. SpringCloud主要项目**

**Spring Cloud Config**

**Spring Cloud Netflix(重点，这些组件用的最多)**

**Spring Cloud Bus**

**Spring Cloud Consul**

**Spring Cloud SecuritySpring Cloud Sleuth**

**Spring Cloud Stream**

**Spring Cloud Task**

**Spring Cloud Zookeeper**

**Spring Cloud Gateway**

**Spring Cloud OpenFeign**

**Spring Cloud的版本关系**

#### **48\. Spring Cloud和SpringBoot版本对应关系**

#### **49\. Spring Cloud和各子项目版本对应关系**

