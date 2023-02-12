
## Spring 基础

### 1. 什么是 Spring 框架?

Spring 是一款开源的轻量级 Java 开发框架，旨在提高开发人员的开发效率以及系统的可维护性。

我们一般说 Spring 框架指的都是 Spring Framework，它是很多模块的集合，使用这些模块可以很方便地协助我们进行开发，比如说 Spring 支持 IoC（Inversion of Control:控制反转） 和 AOP(Aspect-Oriented Programming:面向切面编程)、可以很方便地对数据库进行访问、可以很方便地集成第三方组件（电子邮件，任务，调度，缓存等等）、对单元测试支持比较好、支持 RESTful Java 应用程序的开发。

![](https://img-blog.csdnimg.cn/38ef122122de4375abcd27c3de8f60b4.png)

Spring 最核心的思想就是不重新造轮子，开箱即用，提高开发效率。

Spring 翻译过来就是春天的意思，可见其目标和使命就是为 Java 程序员带来春天啊！感动！

🤐 多提一嘴 ： **语言的流行通常需要一个杀手级的应用，Spring 就是 Java 生态的一个杀手级的应用框架。**

Spring 提供的核心功能主要是 IoC 和 AOP。学习 Spring ，一定要把 IoC 和 AOP 的核心思想搞懂！

+   Spring 官网：[https://spring.io/open in new window](https://spring.io/)
+   Github 地址： https://github.com/spring-projects/spring-framework

### Spring 包含的模块有哪些？

**Spring4.x 版本** ：

![Spring4.x主要模块](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/system-design/framework/spring/jvme0c60b4606711fc4a0b6faf03230247a.png)

**Spring5.x 版本** ：

![Spring5.x主要模块](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/system-design/framework/spring/20200831175708.png)

Spring5.x 版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。

Spring 各个模块的依赖关系如下：

![Spring 各个模块的依赖关系](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/system-design/framework/spring/20200902100038.png)

#### Core Container

Spring 框架的核心模块，也可以说是基础模块，主要提供 IoC 依赖注入功能的支持。Spring 其他所有的功能基本都需要依赖于该模块，我们从上面那张 Spring 各个模块的依赖关系图就可以看出来。

+   **spring-core** ：Spring 框架基本的核心工具类。
+   **spring-beans** ：提供对 bean 的创建、配置和管理等功能的支持。
+   **spring-context** ：提供对国际化、事件传播、资源加载等功能的支持。
+   **spring-expression** ：提供对表达式语言（Spring Expression Language） SpEL 的支持，只依赖于 core 模块，不依赖于其他模块，可以单独使用。

#### AOP

+   **spring-aspects** ：该模块为与 AspectJ 的集成提供支持。
+   **spring-aop** ：提供了面向切面的编程实现。
+   **spring-instrument** ：提供了为 JVM 添加代理（agent）的功能。 具体来讲，它为 Tomcat 提供了一个织入代理，能够为 Tomcat 传递类文 件，就像这些文件是被类加载器加载的一样。没有理解也没关系，这个模块的使用场景非常有限。

#### Data Access/Integration

+   **spring-jdbc** ：提供了对数据库访问的抽象 JDBC。不同的数据库都有自己独立的 API 用于操作数据库，而 Java 程序只需要和 JDBC API 交互，这样就屏蔽了数据库的影响。
+   **spring-tx** ：提供对事务的支持。
+   **spring-orm** ： 提供对 Hibernate、JPA 、iBatis 等 ORM 框架的支持。
+   **spring-oxm** ：提供一个抽象层支撑 OXM(Object-to-XML-Mapping)，例如：JAXB、Castor、XMLBeans、JiBX 和 XStream 等。
+   **spring-jms** : 消息服务。自 Spring Framework 4.1 以后，它还提供了对 spring-messaging 模块的继承。

#### Spring Web

+   **spring-web** ：对 Web 功能的实现提供一些最基础的支持。
+   **spring-webmvc** ： 提供对 Spring MVC 的实现。
+   **spring-websocket** ： 提供了对 WebSocket 的支持，WebSocket 可以让客户端和服务端进行双向通信。
+   **spring-webflux** ：提供对 WebFlux 的支持。WebFlux 是 Spring Framework 5.0 中引入的新的响应式框架。与 Spring MVC 不同，它不需要 Servlet API，是完全异步。

#### Messaging

**spring-messaging** 是从 Spring4.0 开始新加入的一个模块，主要职责是为 Spring 框架集成一些基础的报文传送应用。

#### Spring Test

Spring 团队提倡测试驱动开发（TDD）。有了控制反转 (IoC)的帮助，单元测试和集成测试变得更简单。

Spring 的测试模块对 JUnit（单元测试框架）、TestNG（类似 JUnit）、Mockito（主要用来 Mock 对象）、PowerMock（解决 Mockito 的问题比如无法模拟 final, static， private 方法）等等常用的测试框架支持的都比较好。

### Spring,Spring MVC,Spring Boot 之间什么关系?

很多人对 Spring,Spring MVC,Spring Boot 这三者傻傻分不清楚！这里简单介绍一下这三者，其实很简单，没有什么高深的东西。

Spring 包含了多个功能模块（上面刚刚提到过），其中最重要的是 Spring-Core（主要提供 IoC 依赖注入功能的支持） 模块， Spring 中的其他模块（比如 Spring MVC）的功能实现基本都需要依赖于该模块。

下图对应的是 Spring4.x 版本。目前最新的 5.x 版本中 Web 模块的 Portlet 组件已经被废弃掉，同时增加了用于异步响应式处理的 WebFlux 组件。

![Spring主要模块](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/jvme0c60b4606711fc4a0b6faf03230247a.png)

Spring MVC 是 Spring 中的一个很重要的模块，主要赋予 Spring 快速构建 MVC 架构的 Web 程序的能力。MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，其核心思想是通过将业务逻辑、数据、显示分离来组织代码。

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/image-20210809181452421.png)

使用 Spring 进行开发各种配置过于麻烦比如开启某些 Spring 特性时，需要用 XML 或 Java 进行显式配置。于是，Spring Boot 诞生了！

Spring 旨在简化 J2EE 企业应用程序开发。Spring Boot 旨在简化 Spring 开发（减少配置文件，开箱即用！）。

Spring Boot 只是简化了配置，如果你需要构建 MVC 架构的 Web 程序，你还是需要使用 Spring MVC 作为 MVC 框架，只是说 Spring Boot 帮你简化了 Spring MVC 的很多配置，真正做到开箱即用！

## Spring IoC

### 2. 谈谈自己对于 Spring IoC 的了解

**IoC（Inversion of Control:控制反转）** 是一种设计思想，而不是一个具体的技术实现。IoC 的思想就是将原本在程序中手动创建对象的控制权，交由 Spring 框架来管理。不过， IoC 并非 Spring 特有，在其他语言中也有应用。

**为什么叫控制反转？**

+   **控制** ：指的是对象创建（实例化、管理）的权力
+   **反转** ：控制权交给外部环境（Spring 框架、IoC 容器）

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/frc-365faceb5697f04f31399937c059c162.png)

将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。

在实际项目中一个 Service 类可能依赖了很多其他的类，假如我们需要实例化这个 Service，你可能要每次都要搞清这个 Service 所有底层类的构造函数，这可能会把人逼疯。如果利用 IoC 的话，你只需要配置好，然后在需要的地方引用就行了，这大大增加了项目的可维护性且降低了开发难度。

在 Spring 中， IoC 容器是 Spring 用来实现 IoC 的载体， IoC 容器实际上就是个 Map（key，value），Map 中存放的是各种对象。

Spring 时代我们一般通过 XML 文件来配置 Bean，后来开发人员觉得 XML 文件来配置不太好，于是 SpringBoot 注解配置就慢慢开始流行起来。

相关阅读：

+   [IoC 源码阅读open in new window](https://javadoop.com/post/spring-ioc)
+   [面试被问了几百遍的 IoC 和 AOP ，还在傻傻搞不清楚？open in new window](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486938&idx=1&sn=c99ef0233f39a5ffc1b98c81e02dfcd4&chksm=cea24211f9d5cb07fa901183ba4d96187820713a72387788408040822ffb2ed575d28e953ce7&token=1736772241&lang=zh_CN#rd)

### 3. 什么是 Spring Bean？

简单来说，Bean 代指的就是那些被 IoC 容器所管理的对象。

我们需要告诉 IoC 容器帮助我们管理哪些对象，这个是通过配置元数据来定义的。配置元数据可以是 XML 文件、注解或者 Java 配置类。

```xml
<!-- Constructor-arg with 'value' attribute -->
<bean id="..." class="...">
   <constructor-arg value="..."/>
</bean>
```

下图简单地展示了 IoC 容器如何使用配置元数据来管理对象。

![](https://img-blog.csdnimg.cn/062b422bd7ac4d53afd28fb74b2bc94d.png)

`org.springframework.beans`和 `org.springframework.context` 这两个包是 IoC 实现的基础，如果想要研究 IoC 相关的源码的话，可以去看看

### 4. 将一个类声明为 Bean 的注解有哪些?

+   `@Component` ：通用的注解，可标注任意类为 `Spring` 组件。如果一个 Bean 不知道属于哪个层，可以使用`@Component` 注解标注。
+   `@Repository` : 对应持久层即 Dao 层，主要用于数据库相关操作。
+   `@Service` : 对应服务层，主要涉及一些复杂的逻辑，需要用到 Dao 层。
+   `@Controller` : 对应 Spring MVC 控制层，主要用户接受用户请求并调用 Service 层返回数据给前端页面。

### 5. @Component 和 @Bean 的区别是什么？

+   `@Component` 注解作用于类，而`@Bean`注解作用于方法。
+   `@Component`通常是通过类路径扫描来自动侦测以及自动装配到 Spring 容器中（我们可以使用 `@ComponentScan` 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。`@Bean` 注解通常是我们在标有该注解的方法中定义产生这个 bean,`@Bean`告诉了 Spring 这是某个类的实例，当我需要用它的时候还给我。
+   `@Bean` 注解比 `@Component` 注解的自定义性更强，而且很多地方我们只能通过 `@Bean` 注解来注册 bean。比如当我们引用第三方库中的类需要装配到 `Spring`容器时，则只能通过 `@Bean`来实现。

`@Bean`注解使用示例：

```java
@Configuration
public class AppConfig {
    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }

}
```

上面的代码相当于下面的 xml 配置

```xml
<beans>
    <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```

下面这个例子是通过 `@Component` 无法实现的。

```java
@Bean
public OneService getService(status) {
    case (status)  {
        when 1:
                return new serviceImpl1();
        when 2:
                return new serviceImpl2();
        when 3:
                return new serviceImpl3();
    }
}
```

### 6. 注入 Bean 的注解有哪些？

Spring 内置的 `@Autowired` 以及 JDK 内置的 `@Resource` 和 `@Inject` 都可以用于注入 Bean。

| Annotaion | Package | Source |
| --- | --- | --- |
| `@Autowired` | `org.springframework.bean.factory` | Spring 2.5+ |
| `@Resource` | `javax.annotation` | Java JSR-250 |
| `@Inject` | `javax.inject` | Java JSR-330 |

`@Autowired` 和`@Resource`使用的比较多一些。

### 7. @Autowired 和 @Resource 的区别是什么？

`Autowired` 属于 Spring 内置的注解，默认的注入方式为`byType`（根据类型进行匹配），也就是说会优先根据接口类型去匹配并注入 Bean （接口的实现类）。

**这会有什么问题呢？** 当一个接口存在多个实现类的话，`byType`这种方式就无法正确注入对象了，因为这个时候 Spring 会同时找到多个满足条件的选择，默认情况下它自己不知道选择哪一个。

这种情况下，注入方式会变为 `byName`（根据名称进行匹配），这个名称通常就是类名（首字母小写）。就比如说下面代码中的 `smsService` 就是我这里所说的名称，这样应该比较好理解了吧。

```java
// smsService 就是我们上面所说的名称
@Autowired
private SmsService smsService;
```

举个例子，`SmsService` 接口有两个实现类: `SmsServiceImpl1`和 `SmsServiceImpl2`，且它们都已经被 Spring 容器所管理。

```java
// 报错，byName 和 byType 都无法匹配到 bean
@Autowired
private SmsService smsService;
// 正确注入 SmsServiceImpl1 对象对应的 bean
@Autowired
private SmsService smsServiceImpl1;
// 正确注入  SmsServiceImpl1 对象对应的 bean
// smsServiceImpl1 就是我们上面所说的名称
@Autowired
@Qualifier(value = "smsServiceImpl1")
private SmsService smsService;
```

我们还是建议通过 `@Qualifier` 注解来显式指定名称而不是依赖变量的名称。

`@Resource`属于 JDK 提供的注解，默认注入方式为 `byName`。如果无法通过名称匹配到对应的 Bean 的话，注入方式会变为`byType`。

`@Resource` 有两个比较重要且日常开发常用的属性：`name`（名称）、`type`（类型）。

```java
public @interface Resource {
    String name() default "";
    Class<?> type() default Object.class;
}
```

如果仅指定 `name` 属性则注入方式为`byName`，如果仅指定`type`属性则注入方式为`byType`，如果同时指定`name` 和`type`属性（不建议这么做）则注入方式为`byType`+`byName`。

```java
// 报错，byName 和 byType 都无法匹配到 bean
@Resource
private SmsService smsService;
// 正确注入 SmsServiceImpl1 对象对应的 bean
@Resource
private SmsService smsServiceImpl1;
// 正确注入 SmsServiceImpl1 对象对应的 bean（比较推荐这种方式）
@Resource(name = "smsServiceImpl1")
private SmsService smsService;
```

简单总结一下：

+   **`@Autowired` 是 Spring 提供的注解，`@Resource` 是 JDK 提供的注解**。
+   `Autowired` 默认的注入方式为`byType`（根据类型进行匹配），`@Resource`默认注入方式为 `byName`（根据名称进行匹配）。
+   当一个接口存在多个实现类的情况下，`@Autowired` 和`@Resource`都需要通过名称才能正确匹配到对应的 Bean。`Autowired` 可以通过 `@Qualifier` 注解来显式指定名称，`@Resource`可以通过 `name` 属性来显式指定名称。
+   注入方式不同，@Autowired 支持属性注入、构造方法注入和 Setter 注入，而 @Resource 只支持属性注入和 Setter 注入，当使用 @Resource 实现构造方法注入时就会提示以下错误：
![20230212181731](https://img.ggball.top/picGo/20230212181731.png)

### 8. Bean 的作用域有哪些?

Spring 中 Bean 的作用域通常有下面几种：

+   **singleton** : IoC 容器中只有唯一的 bean 实例。Spring 中的 bean 默认都是单例的，是对单例设计模式的应用。
+   **prototype** : 每次获取都会创建一个新的 bean 实例。也就是说，连续 `getBean()` 两次，得到的是不同的 Bean 实例。
+   **request** （仅 Web 应用可用）: 每一次 HTTP 请求都会产生一个新的 bean（请求 bean），该 bean 仅在当前 HTTP request 内有效。
+   **session** （仅 Web 应用可用） : 每一次来自新 session 的 HTTP 请求都会产生一个新的 bean（会话 bean），该 bean 仅在当前 HTTP session 内有效。
+   **application/global-session** （仅 Web 应用可用）： 每个 Web 应用在启动时创建一个 Bean（应用 Bean），该 bean 仅在当前应用启动时间内有效。
+   **websocket** （仅 Web 应用可用）：每一次 WebSocket 会话产生一个新的 bean。

**如何配置 bean 的作用域呢？**

xml 方式：

```xml
<bean id="..." class="..." scope="singleton"></bean>
```

注解方式：

```java
@Bean
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public Person personPrototype() {
    return new Person();
}
```

### 9. 单例 Bean 的线程安全问题了解吗？

大部分时候我们并没有在项目中使用多线程，所以很少有人会关注这个问题。单例 Bean 存在线程问题，主要是因为当多个线程操作同一个对象的时候是存在资源竞争的。

常见的有两种解决办法：

1.  在 Bean 中尽量避免定义可变的成员变量。
2.  在类中定义一个 `ThreadLocal` 成员变量，将需要的可变成员变量保存在 `ThreadLocal` 中（推荐的一种方式）。

不过，大部分 Bean 实际都是无状态（没有实例变量）的（比如 Dao、Service），这种情况下， Bean 是线程安全的。

### 10. Bean 的生命周期了解么?

> 下面的内容整理自：[https://yemengying.com/2016/07/14/spring-bean-life-cycle/open in new window](https://yemengying.com/2016/07/14/spring-bean-life-cycle/) ，除了这篇文章，再推荐一篇很不错的文章 ：[https://www.cnblogs.com/zrtqsk/p/3735273.htmlopen in new window](https://www.cnblogs.com/zrtqsk/p/3735273.html) 。

+   Bean 容器找到配置文件中 Spring Bean 的定义。
+   Bean 容器利用 Java Reflection API 创建一个 Bean 的实例。
+   如果涉及到一些属性值 利用 `set()`方法设置一些属性值。
+   如果 Bean 实现了 `BeanNameAware` 接口，调用 `setBeanName()`方法，传入 Bean 的名字。
+   如果 Bean 实现了 `BeanClassLoaderAware` 接口，调用 `setBeanClassLoader()`方法，传入 `ClassLoader`对象的实例。
+   如果 Bean 实现了 `BeanFactoryAware` 接口，调用 `setBeanFactory()`方法，传入 `BeanFactory`对象的实例。
+   与上面的类似，如果实现了其他 `*.Aware`接口，就调用相应的方法。
+   如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessBeforeInitialization()` 方法
+   如果 Bean 实现了`InitializingBean`接口，执行`afterPropertiesSet()`方法。
+   如果 Bean 在配置文件中的定义包含 init-method 属性，执行指定的方法。
+   如果有和加载这个 Bean 的 Spring 容器相关的 `BeanPostProcessor` 对象，执行`postProcessAfterInitialization()` 方法
+   当要销毁 Bean 的时候，如果 Bean 实现了 `DisposableBean` 接口，执行 `destroy()` 方法。
+   当要销毁 Bean 的时候，如果 Bean 在配置文件中的定义包含 destroy-method 属性，执行指定的方法。

图示：

![Spring Bean 生命周期](https://images.xiaozhuanlan.com/photo/2019/24bc2bad3ce28144d60d9e0a2edf6c7f.jpg)

与之比较类似的中文版本:

![Spring Bean 生命周期](https://images.xiaozhuanlan.com/photo/2019/b5d264565657a5395c2781081a7483e1.jpg)

## Spring AoP

### 11. 谈谈自己对于 AOP 的了解

AOP(Aspect-Oriented Programming:面向切面编程)能够将那些与业务无关，却为业务模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性。

Spring AOP 就是基于动态代理的，如果要代理的对象，实现了某个接口，那么 Spring AOP 会使用 **JDK Proxy**，去创建代理对象，而对于没有实现接口的对象，就无法使用 JDK Proxy 去进行代理了，这时候 Spring AOP 会使用 **Cglib** 生成一个被代理对象的子类来作为代理，如下图所示：

![SpringAOPProcess](https://img-blog.csdnimg.cn/img_convert/230ae587a322d6e4d09510161987d346.jpeg)

当然你也可以使用 **AspectJ** ！Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。

AOP 切面编程设计到的一些专业术语：

| 术语 | 含义 |
| --- | --- |
| 目标(Target) | 被通知的对象 |
| 代理(Proxy) | 向目标对象应用通知之后创建的代理对象 |
| 连接点(JoinPoint) | 目标对象的所属类中，定义的所有方法均为连接点 |
| 切入点(Pointcut) | 被切面拦截 / 增强的连接点（切入点一定是连接点，连接点不一定是切入点） |
| 通知(Advice) | 增强的逻辑 / 代码，也即拦截到目标对象的连接点之后要做的事情 |
| 切面(Aspect) | 切入点(Pointcut)+通知(Advice) |
| Weaving(织入) | 将通知应用到目标对象，进而生成代理对象的过程动作 |

### 12. Spring AOP 和 AspectJ AOP 有什么区别？

**Spring AOP 属于运行时增强，而 AspectJ 是编译时增强。** Spring AOP 基于代理(Proxying)，而 AspectJ 基于字节码操作(Bytecode Manipulation)。

Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java 生态系统中最完整的 AOP 框架了。AspectJ 相比于 Spring AOP 功能更加强大，但是 Spring AOP 相对来说更简单，

如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ ，它比 Spring AOP 快很多。

### AspectJ 定义的通知类型有哪些？

+   **Before**（前置通知）：目标对象的方法调用之前触发
+   **After** （后置通知）：目标对象的方法调用之后触发
+   **AfterReturning**（返回通知）：目标对象的方法调用完成，在返回结果值之后触发
+   **AfterThrowing**（异常通知） ：目标对象的方法运行中抛出 / 触发异常后触发。AfterReturning 和 AfterThrowing 两者互斥。如果方法调用成功无异常，则会有返回值；如果方法抛出了异常，则不会有返回值。
+   **Around** （环绕通知）：编程式控制目标对象的方法调用。环绕通知是所有通知类型中可操作范围最大的一种，因为它可以直接拿到目标对象，以及要执行的方法，所以环绕通知可以任意的在目标对象的方法调用前后搞事，甚至不调用目标对象的方法

### 多个切面的执行顺序如何控制？

1、通常使用`@Order` 注解直接定义切面顺序

```java
// 值越小优先级越高
@Order(3)
@Component
@Aspect
public class LoggingAspect implements Ordered {
```

**2、实现`Ordered` 接口重写 `getOrder` 方法。**

```java
@Component
@Aspect
public class LoggingAspect implements Ordered {

    // ....

    @Override
    public int getOrder() {
        // 返回值越小优先级越高
        return 1;
    }
}
```

## Spring MVC

### 13. 说说自己对于 Spring MVC 了解?

MVC 是模型(Model)、视图(View)、控制器(Controller)的简写，其核心思想是通过将业务逻辑、数据、显示分离来组织代码。

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/java-guide-blog/image-20210809181452421.png)

网上有很多人说 MVC 不是设计模式，只是软件设计规范，我个人更倾向于 MVC 同样是众多设计模式中的一种。**[java-design-patternsopen in new window](https://github.com/iluwatar/java-design-patterns)** 项目中就有关于 MVC 的相关介绍。

![](https://img-blog.csdnimg.cn/159b3d3e70dd45e6afa81bf06d09264e.png)

想要真正理解 Spring MVC，我们先来看看 Model 1 和 Model 2 这两个没有 Spring MVC 的时代。

**Model 1 时代**

很多学 Java 后端比较晚的朋友可能并没有接触过 Model 1 时代下的 JavaWeb 应用开发。在 Model1 模式下，整个 Web 应用几乎全部用 JSP 页面组成，只用少量的 JavaBean 来处理数据库连接、访问等操作。

这个模式下 JSP 即是控制层（Controller）又是表现层（View）。显而易见，这种模式存在很多问题。比如控制逻辑和表现逻辑混杂在一起，导致代码重用率极低；再比如前端和后端相互依赖，难以进行测试维护并且开发效率极低。


![mvc-mode1](https://img.ggball.top/picGo/mvc-mode1.png)

**Model 2 时代**

学过 Servlet 并做过相关 Demo 的朋友应该了解“Java Bean(Model)+ JSP（View）+Servlet（Controller） ”这种开发模式，这就是早期的 JavaWeb MVC 开发模式。

+   Model:系统涉及的数据，也就是 dao 和 bean。
+   View：展示模型中的数据，只是用来展示。
+   Controller：处理用户请求都发送给 ，返回数据给 JSP 并展示给用户。

![mvc-model2](https://img.ggball.top/picGo/mvc-model2.png)

Model2 模式下还存在很多问题，Model2 的抽象和封装程度还远远不够，使用 Model2 进行开发时不可避免地会重复造轮子，这就大大降低了程序的可维护性和复用性。

于是，很多 JavaWeb 开发相关的 MVC 框架应运而生比如 Struts2，但是 Struts2 比较笨重。

**Spring MVC 时代**

随着 Spring 轻量级开发框架的流行，Spring 生态圈出现了 Spring MVC 框架， Spring MVC 是当前最优秀的 MVC 框架。相比于 Struts2 ， Spring MVC 使用更加简单和方便，开发效率更高，并且 Spring MVC 运行速度更快。

MVC 是一种设计模式，Spring MVC 是一款很优秀的 MVC 框架。Spring MVC 可以帮助我们进行更简洁的 Web 层的开发，并且它天生与 Spring 框架集成。Spring MVC 下我们一般把后端项目分为 Service 层（处理业务）、Dao 层（数据库操作）、Entity 层（实体类）、Controller 层(控制层，返回数据给前台页面)。

### 14. Spring MVC 的核心组件有哪些？

记住了下面这些组件，也就记住了 SpringMVC 的工作原理。

+   **`DispatcherServlet`** ：**核心的中央处理器**，负责接收请求、分发，并给予客户端响应。
+   **`HandlerMapping`** ：**处理器映射器**，根据 uri 去匹配查找能处理的 `Handler` ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
+   **`HandlerAdapter`** ：**处理器适配器**，根据 `HandlerMapping` 找到的 `Handler` ，适配执行对应的 `Handler`；
+   **`Handler`** ：**请求处理器**，处理实际请求的处理器。
+   **`ViewResolver`** ：**视图解析器**，根据 `Handler` 返回的逻辑视图 / 视图，解析并渲染真正的视图，并传递给 `DispatcherServlet` 响应客户端

### 15. SpringMVC 工作原理了解吗?

**Spring MVC 原理如下图所示：**

> SpringMVC 工作原理的图解我没有自己画，直接图省事在网上找了一个非常清晰直观的，原出处不明。

![](https://img-blog.csdnimg.cn/img_convert/de6d2b213f112297298f3e223bf08f28.png)

**流程说明（重要）：**

1.  客户端（浏览器）发送请求， `DispatcherServlet`拦截请求。
2.  `DispatcherServlet` 根据请求信息调用 `HandlerMapping` 。`HandlerMapping` 根据 uri 去匹配查找能处理的 `Handler`（也就是我们平常说的 `Controller` 控制器） ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
3.  `DispatcherServlet` 调用 `HandlerAdapter`适配执行 `Handler` 。
4.  `Handler` 完成对用户请求的处理后，会返回一个 `ModelAndView` 对象给`DispatcherServlet`，`ModelAndView` 顾名思义，包含了数据模型以及相应的视图的信息。`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
5.  `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
6.  `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
7.  把 `View` 返回给请求者（浏览器）

### 16. 统一异常处理怎么做？

推荐使用注解的方式统一异常处理，具体会使用到 `@ControllerAdvice` + `@ExceptionHandler` 这两个注解 。

```java
@ControllerAdvice
@ResponseBody
public class GlobalExceptionHandler {

    @ExceptionHandler(BaseException.class)
    public ResponseEntity<?> handleAppException(BaseException ex, HttpServletRequest request) {
      //......
    }

    @ExceptionHandler(value = ResourceNotFoundException.class)
    public ResponseEntity<ErrorReponse> handleResourceNotFoundException(ResourceNotFoundException ex, HttpServletRequest request) {
      //......
    }
}
```

这种异常处理方式下，会给所有或者指定的 `Controller` 织入异常处理的逻辑（AOP），当 `Controller` 中的方法抛出异常的时候，由被`@ExceptionHandler` 注解修饰的方法进行处理。

`ExceptionHandlerMethodResolver` 中 `getMappedMethod` 方法决定了异常具体被哪个被 `@ExceptionHandler` 注解修饰的方法处理异常。

```java
@Nullable
	private Method getMappedMethod(Class<? extends Throwable> exceptionType) {
		List<Class<? extends Throwable>> matches = new ArrayList<>();
    //找到可以处理的所有异常信息。mappedMethods 中存放了异常和处理异常的方法的对应关系
		for (Class<? extends Throwable> mappedException : this.mappedMethods.keySet()) {
			if (mappedException.isAssignableFrom(exceptionType)) {
				matches.add(mappedException);
			}
		}
    // 不为空说明有方法处理异常
		if (!matches.isEmpty()) {
      // 按照匹配程度从小到大排序
			matches.sort(new ExceptionDepthComparator(exceptionType));
      // 返回处理异常的方法
			return this.mappedMethods.get(matches.get(0));
		}
		else {
			return null;
		}
	}
```

从源代码看出： **`getMappedMethod()`会首先找到可以匹配处理异常的所有方法信息，然后对其进行从小到大的排序，最后取最小的那一个匹配的方法(即匹配度最高的那个)。**

### 17. Spring 框架中用到了哪些设计模式？

> 关于下面这些设计模式的详细介绍，可以看我写的 [Spring 中的设计模式详解open in new window](https://javaguide.cn/system-design/framework/spring/spring-design-patterns-summary.html) 这篇文章。

+   **工厂设计模式** : Spring 使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。
+   **代理设计模式** : Spring AOP 功能的实现。
+   **单例设计模式** : Spring 中的 Bean 默认都是单例的。
+   **模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
+   **包装器设计模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
+   **观察者模式:** Spring 事件驱动模型就是观察者模式很经典的一个应用。
+   **适配器模式** : Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配`Controller`。
+   ......

## Spring 事务

关于 Spring 事务的详细介绍，可以看我写的 [Spring 事务详解open in new window](https://javaguide.cn/system-design/framework/spring/spring-transaction.html) 这篇文章。

### 18. Spring 管理事务的方式有几种？

+   **编程式事务** ： 在代码中硬编码(不推荐使用) : 通过 `TransactionTemplate`或者 `TransactionManager` 手动管理事务，实际应用中很少使用，但是对于你理解 Spring 事务管理原理有帮助。
+   **声明式事务** ： 在 XML 配置文件中配置或者直接基于注解（推荐使用） : 实际是通过 AOP 实现（基于`@Transactional` 的全注解方式使用最多）

### 19. Spring 事务中哪几种事务传播行为?

**事务传播行为是为了解决业务层方法之间互相调用的事务问题**。

当事务方法被另一个事务方法调用时，必须指定事务应该如何传播。例如：方法可能继续在现有事务中运行，也可能开启一个新事务，并在自己的事务中运行。

正确的事务传播行为可能的值如下:

**1.`TransactionDefinition.PROPAGATION_REQUIRED`**

使用的最多的一个事务传播行为，我们平时经常使用的`@Transactional`注解默认使用就是这个事务传播行为。如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新的事务。

**`2.TransactionDefinition.PROPAGATION_REQUIRES_NEW`**

创建一个新的事务，如果当前存在事务，则把当前事务挂起。也就是说不管外部方法是否开启事务，`Propagation.REQUIRES_NEW`修饰的内部方法会新开启自己的事务，且开启的事务相互独立，互不干扰。

**3.`TransactionDefinition.PROPAGATION_NESTED`**

如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于`TransactionDefinition.PROPAGATION_REQUIRED`。

**4.`TransactionDefinition.PROPAGATION_MANDATORY`**

如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。（mandatory：强制性）

这个使用的很少。

若是错误的配置以下 3 种事务传播行为，事务将不会发生回滚：

+   **`TransactionDefinition.PROPAGATION_SUPPORTS`**: 如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务的方式继续运行。
+   **`TransactionDefinition.PROPAGATION_NOT_SUPPORTED`**: 以非事务方式运行，如果当前存在事务，则把当前事务挂起。
+   **`TransactionDefinition.PROPAGATION_NEVER`**: 以非事务方式运行，如果当前存在事务，则抛出异常。

### 20. Spring 事务中的隔离级别有哪几种?

和事务传播行为这块一样，为了方便使用，Spring 也相应地定义了一个枚举类：`Isolation`

```java
public enum Isolation {

    DEFAULT(TransactionDefinition.ISOLATION_DEFAULT),

    READ_UNCOMMITTED(TransactionDefinition.ISOLATION_READ_UNCOMMITTED),

    READ_COMMITTED(TransactionDefinition.ISOLATION_READ_COMMITTED),

    REPEATABLE_READ(TransactionDefinition.ISOLATION_REPEATABLE_READ),

    SERIALIZABLE(TransactionDefinition.ISOLATION_SERIALIZABLE);

    private final int value;

    Isolation(int value) {
        this.value = value;
    }

    public int value() {
        return this.value;
    }

}
```

下面我依次对每一种事务隔离级别进行介绍：

+   **`TransactionDefinition.ISOLATION_DEFAULT`** :使用后端数据库默认的隔离级别，MySQL 默认采用的 `REPEATABLE_READ` 隔离级别 Oracle 默认采用的 `READ_COMMITTED` 隔离级别.
+   **`TransactionDefinition.ISOLATION_READ_UNCOMMITTED`** :最低的隔离级别，使用这个隔离级别很少，因为它允许读取尚未提交的数据变更，**可能会导致脏读、幻读或不可重复读**
+   **`TransactionDefinition.ISOLATION_READ_COMMITTED`** : 允许读取并发事务已经提交的数据，**可以阻止脏读，但是幻读或不可重复读仍有可能发生**
+   **`TransactionDefinition.ISOLATION_REPEATABLE_READ`** : 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，**可以阻止脏读和不可重复读，但幻读仍有可能发生。**
+   **`TransactionDefinition.ISOLATION_SERIALIZABLE`** : 最高的隔离级别，完全服从 ACID 的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，**该级别可以防止脏读、不可重复读以及幻读**。但是这将严重影响程序的性能。通常情况下也不会用到该级别。

### 12. @Transactional(rollbackFor = Exception.class)注解了解吗？

`Exception` 分为运行时异常 `RuntimeException` 和非运行时异常。事务管理对于企业应用来说是至关重要的，即使出现异常情况，它也可以保证数据的一致性。

当 `@Transactional` 注解作用于类上时，该类的所有 public 方法将都具有该类型的事务属性，同时，我们也可以在方法级别使用该标注来覆盖类级别的定义。如果类或者方法加了这个注解，那么这个类里面的方法抛出异常，就会回滚，数据库里面的数据也会回滚。

在 `@Transactional` 注解中如果不配置`rollbackFor`属性,那么事务只会在遇到`RuntimeException`的时候才会回滚，加上 `rollbackFor=Exception.class`,可以让事务在遇到非运行时异常时也回滚。

## Spring Data JPA

JPA 重要的是实战，这里仅对小部分知识点进行总结。

### 22. 如何使用 JPA 在数据库中非持久化一个字段？

假如我们有下面一个类：

```java
@Entity(name="USER")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    @Column(name = "ID")
    private Long id;

    @Column(name="USER_NAME")
    private String userName;

    @Column(name="PASSWORD")
    private String password;

    private String secrect;

}
```

如果我们想让`secrect` 这个字段不被持久化，也就是不被数据库存储怎么办？我们可以采用下面几种方法：

```java
static String transient1; // not persistent because of static
final String transient2 = "Satish"; // not persistent because of final
transient String transient3; // not persistent because of transient
@Transient
String transient4; // not persistent because of @Transient
```

一般使用后面两种方式比较多，我个人使用注解的方式比较多。

### JPA 的审计功能是做什么的？有什么用？

审计功能主要是帮助我们记录数据库操作的具体行为比如某条记录是谁创建的、什么时间创建的、最后修改人是谁、最后修改时间是什么时候。

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@MappedSuperclass
@EntityListeners(value = AuditingEntityListener.class)
public abstract class AbstractAuditBase {

    @CreatedDate
    @Column(updatable = false)
    @JsonIgnore
    private Instant createdAt;

    @LastModifiedDate
    @JsonIgnore
    private Instant updatedAt;

    @CreatedBy
    @Column(updatable = false)
    @JsonIgnore
    private String createdBy;

    @LastModifiedBy
    @JsonIgnore
    private String updatedBy;
}
```

+   `@CreatedDate`: 表示该字段为创建时间字段，在这个实体被 insert 的时候，会设置值
    
+   `@CreatedBy` :表示该字段为创建人，在这个实体被 insert 的时候，会设置值
    
    `@LastModifiedDate`、`@LastModifiedBy`同理。
    

### 23. 实体之间的关联关系注解有哪些？

+   `@OneToOne` : 一对一。
+   `@ManyToMany` ：多对多。
+   `@OneToMany` : 一对多。
+   `@ManyToOne` ：多对一。

利用 `@ManyToOne` 和 `@OneToMany` 也可以表达多对多的关联关系。

## Spring Security

Spring Security 重要的是实战，这里仅对小部分知识点进行总结。

### 24. 有哪些控制请求访问权限的方法？

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/system-design/framework/spring/image-20220728201854641.png)

+   `permitAll()` ：无条件允许任何形式访问，不管你登录还是没有登录。
+   `anonymous()` ：允许匿名访问，也就是没有登录才可以访问。
+   `denyAll()` ：无条件决绝任何形式的访问。
+   `authenticated()`：只允许已认证的用户访问。
+   `fullyAuthenticated()` ：只允许已经登录或者通过 remember-me 登录的用户访问。
+   `hasRole(String)` : 只允许指定的角色访问。
+   `hasAnyRole(String)` : 指定一个或者多个角色，满足其一的用户即可访问。
+   `hasAuthority(String)` ：只允许具有指定权限的用户访问
+   `hasAnyAuthority(String)` ：指定一个或者多个权限，满足其一的用户即可访问。
+   `hasIpAddress(String)` : 只允许指定 ip 的用户访问。

### 25. hasRole 和 hasAuthority 有区别吗？

可以看看松哥的这篇文章：[Spring Security 中的 hasRole 和 hasAuthority 有区别吗？open in new window](https://mp.weixin.qq.com/s/GTNOa2k9_n_H0w24upClRw)，介绍的比较详细。

### 26. 如何对密码进行加密？

如果我们需要保存密码这类敏感数据到数据库的话，需要先加密再保存。

Spring Security 提供了多种加密算法的实现，开箱即用，非常方便。这些加密算法实现类的父类是 `PasswordEncoder` ，如果你想要自己实现一个加密算法的话，也需要继承 `PasswordEncoder`。

`PasswordEncoder` 接口一共也就 3 个必须实现的方法。

```java
public interface PasswordEncoder {
    // 加密也就是对原始密码进行编码
    String encode(CharSequence var1);
    // 比对原始密码和数据库中保存的密码
    boolean matches(CharSequence var1, String var2);
    // 判断加密密码是否需要再次进行加密，默认返回 false
    default boolean upgradeEncoding(String encodedPassword) {
        return false;
    }
}
```

![](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/system-design/framework/spring/image-20220728183540954.png)

官方推荐使用基于 bcrypt 强哈希函数的加密算法实现类。

### 27. 如何优雅更换系统使用的加密算法？

如果我们在开发过程中，突然发现现有的加密算法无法满足我们的需求，需要更换成另外一个加密算法，这个时候应该怎么办呢？

推荐的做法是通过 `DelegatingPasswordEncoder` 兼容多种不同的密码加密方案，以适应不同的业务需求。

从名字也能看出来，`DelegatingPasswordEncoder` 其实就是一个代理类，并非是一种全新的加密算法，它做的事情就是代理上面提到的加密算法实现类。在 Spring Security 5.0之后，默认就是基于 `DelegatingPasswordEncoder` 进行密码加密的。




### 28.什么是 Spring 框架？Spring 框架有哪些主要模块？
Spring 框架是一个为 Java 应用程序的开发提供了综合、广泛的基础性支持的 Java 平台。


Spring 帮助开发者解决了开发中基础性的问题，使得开发人员可以专注于应用程序的开发。
Spring 框架本身亦是按照设计模式精心打造，这使得我们可以在开发环境中安心的集成 Spring 框架，不必担心 Spring 是如何在后台进行工作的。
Spring 框架至今已集成了 20 多个模块。这些模块主要被分如下图所示的核心容器、数据访问/集成,、Web、AOP（面向切面编程）、工具、消息和测试模块。




### 29. 使用 Spring 框架能带来哪些好处？

下面列举了一些使用 Spring 框架带来的主要好处：
•	Dependency Injection(DI) 方法使得构造器和 JavaBean properties 文件中的依赖关系一目了然。
•	与 EJB 容器相比较，IoC 容器更加趋向于轻量级。这样一来 IoC 容器在有限的内存和 CPU 资源的情况下进行应用程序的开发和发布就变得十分有利。

•	Spring 并没有闭门造车，Spring 利用了已有的技术比如 ORM 框架、logging 框架、J2EE、Q uartz 和 JDK Timer，以及其他视图技术。

•	Spring 框架是按照模块的形式来组织的。由包和类的编号就可以看出其所属的模块，开发者仅仅需要选用他们需要的模块即可。

•	要测试一项用 Spring 开发的应用程序十分简单，因为测试相关的环境代码都已经囊括在框架中了。更加简单的是，利用 JavaBean 形式的 POJO 类，可以很方便的利用依赖注入来写入测试数据。
•	Spring 的 Web 框架亦是一个精心设计的 Web MVC 框架，为开发者们在 web 框架的选择上提供了一个除了主流框架比如 Struts、过度设计的、不流行 web 框架的以外的有力选项。

•	Spring 提供了一个便捷的事务管理接口，适用于小型的本地事物处理（比如在单 DB 的环境下）和复杂的共同事物处理（比如利用 JTA 的复杂 DB 环境）。
### 30. 什么是控制反转(IOC)？什么是依赖注入？
控制反转是应用于软件工程领域中的，在运行时被装配器对象来绑定耦合对象的一种编程技巧，对象之间耦合关系在编译时通常是未知的。在传统的编程方式中，业 务逻辑的流程是由应用程序中的早已被设定好关联关系的对象来决定的。在使用控制反转的情况下，业务逻辑的流程是由对象关系
 
图来决定的，该对象关系图由装配 器负责实例化，这种实现方式还可以将对象之间的关联关系的定义抽象化。而绑定的过程是通过“依赖注入”实现的。
控制反转是一种以给予应用程序中目标组件更多控制为目的设计范式，并在我们的实际工作中起到了有效的作用。
依赖注入是在编译阶段尚未知所需的功能是来自哪个的类的情况下，将其他对象所依赖的功能对象实例化的模式。这就需要一种机制用来激活相应的组件以提供特定的功能，所以依赖注入是控制反转的基础。否则如果在组件不受框架控制的情况下，框架又怎么知道要创建哪个组件？
在 Java 中依然注入有以下三种实现方式：
1.	构造器注入

2.	Setter 方法注入

3.	接口注入

### 31. 请解释下 Spring 框架中的 IoC？
Spring 中的 org.springframework.beans 包和 org.springframework.context 包构成了 Spring 框架 IoC 容器的基础。
BeanFactory 接口提供了一个先进的配置机制，使得任何类型的对象的配置成为可能。ApplicationContex 接口对 BeanFactory（是一个子接口）进行了扩展，在 BeanFactory 的基础上添加了其他功能，比如与 Spring 的 AOP 更容易集成，也提供了处理 message resource的机制（用于国际化）、事件传播以及应用层的特别配置，比如针对 Web 应用的WebApplicationContext。
org.springframework.beans.factory.BeanFactory 是 Spring IoC 容器的具体实现， 用来包装和管理前面提到的各种 bean。BeanFactory 接口是 Spring IoC 容器的核心接口。
IOC:把对象的创建、初始化、销毁交给 spring 来管理，而不是由开发者控制，实现控制反转。



### 32. BeanFactory 和 ApplicationContext 有什么区别？

BeanFactory 可以理解为含有 bean 集合的工厂类。BeanFactory 包含了种 bean 的定义，以便在接收到客户端请求时将对应的 bean 实例化。
BeanFactory 还能在实例化对象的时生成协作类之间的关系。此举将 bean 自身与 bean 客户端的配置中解放出来。BeanFactory 还包含 了 bean 生命周期的控制，调用客户端的初始化方法
（initialization methods）和销毁方法（destruction methods）。
从表面上看，application context 如同 bean factory 一样具有 bean 定义、bean 关联关系的设置，根据请求分发 bean 的功能。但 applicationcontext 在此基础上还提供了其他的功能。
1.	提供了支持国际化的文本消息

2.	统一的资源文件读取方式

3.	已在监听器中注册的 bean 的事件
 
以下是三种较常见的 ApplicationContext 实现方式：
1、ClassPathXmlApplicationContext：从 classpath 的 XML 配置文件中读取上下文，并生成上下文定义。应用程序上下文从程序环境变量中


2、FileSystemXmlApplicationContext ：由文件系统中的 XML 配置文件读取上下文。



3、XmlWebApplicationContext：由 Web 应用的 XML 文件读取上下文。


4.	AnnotationConfigApplicationContext(基于 Java 配置启动容器)









### 33. Spring 有几种配置方式？
 
将 Spring 配置到应用开发中有以下三种方式：
1.	基于 XML 的配置

2.	基于注解的配置

3.	基于 Java 的配置

### 34. 如何用基于 XML 配置的方式配置 Spring？
在 Spring 框架中，依赖和服务需要在专门的配置文件来实现，我常用的 XML 格式的配置文件。这些配置文件的格式通常用<beans>开头，然后一系列的 bean 定义和专门的应用配置选项组成。
SpringXML 配置的主要目的时候是使所有的 Spring 组件都可以用 xml 文件的形式来进行配置。这意味着不会出现其他的 Spring 配置类型（比如声明的方式或基于 Java Class 的配置方式）
Spring 的 XML 配置方式是使用被 Spring 命名空间的所支持的一系列的 XML 标签来实现的。
Spring 有以下主要的命名空间：context、beans、jdbc、tx、aop、mvc 和 aso。如：



下面这个 web.xml 仅仅配置了 DispatcherServlet，这件最简单的配置便能满足应用程序配置运行时组件的需求。
 
 


### 35. 如何用基于 Java 配置的方式配置 Spring？

Spring 对 Java 配置的支持是由@Configuration 注解和@Bean 注解来实现的。由@Bean 注解的方法将会实例化、配置和初始化一个 新对象，这个对象将由 Spring 的 IoC 容器来管理。@Bean 声明所起到的作用与<bean/> 元素类似。被 @Configuration 所注解的类则表示这个类的主要目的是作为 bean 定义的资源。被@Configuration 声明的类可以通过在同一个类的 内部调用@bean 方法来设置嵌入 bean 的依赖关系。
最简单的@Configuration 声明类请参考下面的代码：

对于上面的@Beans 配置文件相同的 XML 配置文件如下：
<beans>     
    <bean id="myService" class="com.somnus.services.MyServiceImpl"/>     
</beans>  


上述配置方式的实例化方式如下：利用 AnnotationConfigApplicationContext 类进行实例化


 
 
要使用组件组建扫描，仅需用@Configuration 进行注解即可：


在上面的例子中，com.acme 包首先会被扫到，然后再容器内查找被@Component 声明的类，找到后将这些类按照 Sring bean 定义进行注册。
如果你要在你的 web 应用开发中选用上述的配置的方式的话，需要用AnnotationConfigWebApplicationContext 类来读 取配置文件，可以用来配置 Spring 的Servlet 监听器 ContextLoaderListener 或者 Spring MVC 的 DispatcherServlet。

<web-app>     
    <!-- Configure ContextLoaderListener to use AnnotationConfigWebApplicationContext     
        instead of the default XmlWebApplicationContext -->     
    <context-param>     
        <param-name>contextClass</param-name>     
        <param-value>     
            org.springframework.web.context.support.AnnotationConfigWebApplicatio nContext     
        </param-value>     
    </context-param>     
      
    <!-- Configuration locations must consist of one or more comma- or space-delimited     
        fully-qualified @Configuration classes. Fully-qualified packages may also be     
        specified for component-scanning -->     
    <context-param>     
        <param-name>contextConfigLocation</param-name>     
        <param-value>com.howtodoinjava.AppConfig</param-value>     
    </context-param>     
      
    <!-- Bootstrap the root application context as usual using ContextLoaderListener -->     
 
    <listener>     
        <listener- class>org.springframework.web.context.ContextLoaderListener</listener
-class>     
    </listener>     
      
    <!-- Declare a Spring MVC DispatcherServlet as usual -->     
    <servlet>     
        <servlet-name>dispatcher</servlet-name>     
        <servlet- class>org.springframework.web.servlet.DispatcherServlet</servlet- class>     
        <!-- Configure DispatcherServlet to use AnnotationConfigWebApplicationContext     
            instead of the default XmlWebApplicationContext -->     
        <init-param>     
            <param-name>contextClass</param-name>     
            <param-value>     
                org.springframework.web.context.support.AnnotationConfigWebApplicatio nContext     
            </param-value>     
        </init-param>     
        <!-- Again, config locations must consist of one or more comma- or space-delimited     
            and fully-qualified @Configuration classes -->     
        <init-param>     
            <param-name>contextConfigLocation</param-name>     
            <param-value>com.howtodoinjava.web.MvcConfig</param- value>     
        </init-param>     
    </servlet>     
      
    <!-- map all requests for /app/* to the dispatcher servlet -->     
    <servlet-mapping>     
        <servlet-name>dispatcher</servlet-name>     
        <url-pattern>/app/*</url-pattern>     
    </servlet-mapping>     
</web-app     
 

### 36. 怎样用注解的方式配置 Spring？
Spring 在 2.5 版本以后开始支持用注解的方式来配置依赖注入。可以用注解的方式来替代 XML 方式的 bean 描述，可以将 bean 描述转移到组件类的 内部，只需要在相关类上、方法上或者字段声明上使用注解即可。注解注入将会被容器在 XML 注入之前被处理，所以后者会覆盖掉前者对于同一个属性的处理结 果。
注解装配在 Spring 中是默认关闭的。所以需要在 Spring 文件中配置一下才能使用基于注解的装配模式。如果你想要在你的应用程序中使用关于注解的方法的话，请参考如下的配置。
在 <context:annotation-config/>标签配置完成以后，就可以用注解的方式在 Spring 中向属性、方法和构造方法中自动装配变量。
下面是几种比较重要的注解类型：

1.	@Required：该注解应用于设值方法。

2.	@Autowired：该注解应用于有值设值方法、非设值方法、构造方法和变量。

3.	@Qualifier：该注解和@Autowired 注解搭配使用，用于消除特定 bean 自动装配的歧义。

4.	JSR-250 Annotations：Spring 支持基于 JSR-250 注解的以下注解，@Resource、
@PostConstruct 和 @PreDestroy 。

### 37. 请解释 Spring Bean 的生命周期？
Spring Bean 的生命周期简单易懂。在一个 bean 实例被初始化时，需要执行一系列的初始化操作以达到可用的状态。同样的，当一个 bean 不在被调用时需要进行相关的析构操作，并从 bean 容器中移除。
Spring bean factory 负责管理在 spring 容器中被创建的 bean 的生命周期。Bean 的生命周期由两组回调（call back）方法组成。
1.	初始化之后调用的回调方法。

2.	销毁之前调用的回调方法。

Spring 框架提供了以下四种方式来管理 bean 的生命周期事件：
•	InitializingBean 和 DisposableBean 回调接口

•	针对特殊行为的其他 Aware 接口

•	Bean 配置文件中的 Custom init()方法和 destroy()方法
 
•	@PostConstruct 和@PreDestroy 注解方式

使用 customInit()和 customDestroy()方法管理 bean 生命周期的代码样例如下：
 


### 38. Spring Bean 的作用域之间有什么区别？
Spring 容器中的 bean 可以分为 5 个范围。所有范围的名称都是自说明的，但是为了避免混淆，还是让我们来解释一下：
1.	singleton：这种 bean 范围是默认的，这种范围确保不管接受到多少个请求，每个容器中只有一个
bean 的实例，单例的模式由 bean factory 自身来维护。

2.	prototype：原形范围与单例范围相反，为每一个 bean 请求提供一个实例。

3.	request：在请求 bean 范围内会每一个来自客户端的网络请求创建一个实例，在请求完成以后，
bean 会失效并被垃圾回收器回收。

4.	Session：与请求范围类似，确保每个 session 中有一个 bean 的实例，在 session 过期后，bean
会随之失效。

5.	global- session：global-session 和 Portlet 应用相关。当你的应用部署在 Portlet 容器中工作时，它包含很多 portlet。如果 你想要声明让所有的 portlet 共用全局的存储变量的话，那么这全局变量需要存储在 global-session 中。

全局作用域与 Servlet 中的 session 作用域效果相同。


### 39. 什么是 Spring inner beans？

在 Spring 框架中，无论何时 bean 被使用时，当仅被调用了一个属性。一个明智的做法是将这个bean 声明为内部 bean。内部 bean 可以用 setter 注入“属性”和构造方法注入“构造参数”的方式来实现。
比如，在我们的应用程序中，一个 Customer 类引用了一个 Person 类，我们的要做的是创建一个
Person 的实例，然后在 Customer 内部使用。

 
 







内部 bean 的声明方式如下：




### 40. Spring 框架中的单例 Beans 是线程安全的么？
Spring 框架并没有对单例 bean 进行任何多线程的封装处理。关于单例 bean 的线程安全和并发问题需要开发者自行去搞定。但实际上，大部分的 Spring bean 并没有可变的状态(比如 Serview 类和 DAO 类)，所以在某种程度上说 Spring 的单例 bean 是线程安全的。如果你的 bean 有多种状态的话（比如 View Model 对象），就需要自行保证线程安全。
最浅显的解决办法就是将多态 bean 的作用域由“singleton”变更为“prototype”。
 
### 41. 请举例说明如何在 Spring 中注入一个 Java Collection？

Spring 提供了以下四种集合类的配置元素：
•	<list> :	该标签用来装配可重复的 list 值。

•	<set> :	该标签用来装配没有重复的 set 值。

•	<map>:	该标签可用来注入键和值可以为任何类型的键值对。

•	<props> : 该标签支持注入键和值都是字符串类型的键值对。下面看一下具体的例子：

<beans>     
   <!-- Definition for javaCollection -->     
   <bean id="javaCollection" class="com.howtodoinjava.JavaCollection">     
      <!-- java.util.List -->     
      <property name="customList">     
        <list>     
           <value>INDIA</value>     
           <value>Pakistan</value>     
           <value>USA</value>     
           <value>UK</value>     
        </list>     
      </property>     
      
     <!-- java.util.Set -->     
     <property name="customSet">     
        <set>     
           <value>INDIA</value>     
           <value>Pakistan</value>     
           <value>USA</value>     
           <value>UK</value>     
        </set>     
      </property>     
      
     <!-- java.util.Map -->     
     <property name="customMap">     
        <map>     
           <entry key="1" value="INDIA"/>     
           <entry key="2" value="Pakistan"/>     
           <entry key="3" value="USA"/>     
           <entry key="4" value="UK"/>     
        </map>     
 
 



### 42. 如何向 Spring Bean 中注入一个 Java.util.Properties？
第一种方法是使用如下面代码所示的<props> 标签：


也可用”util:”命名空间来从 properties 文件中创建出一个 propertiesbean，然后利用 setter 方法注入 bean 的引用。


### 43. 请解释 Spring Bean 的自动装配？
 
在 Spring 框架中，在配置文件中设定 bean 的依赖关系是一个很好的机制，Spring 容器还可以自动装配合作关系 bean 之间的关联关系。这意味着 Spring 可以通过向 Bean Factory 中注入的方式自动搞定 bean 之间的依赖关系。自动装配可以设置在每个 bean 上，也可以设定在特定的 bean 上。
下面的 XML 配置文件表明了如何根据名称将一个 bean 设置为自动装配：




除了 bean 配置文件中提供的自动装配模式，还可以使用@Autowired 注解来自动装配指定的 bean。在使用@Autowired 注解之前需要在按照如下的配置方式在 Spring 配置文件进行配置才可以使用。
 


也可以通过在配置文件中配置 AutowiredAnnotationBeanPostProcessor 达到相同的效果。






配置好以后就可以使用@Autowired 来标注了。
 
 

### 44. 请解释自动装配模式的区别？

在 Spring 框架中共有 5 种自动装配，让我们逐一分析。
1.	no：这是 Spring 框架的默认设置，在该设置下自动装配是关闭的，开发者需要自行在 bean 定义中用标签明确的设置依赖关系。

2.	byName：该选项可以根据 bean 名称设置依赖关系。当向一个 bean 中自动装配一个属性时，容器将根据 bean 的名称自动在在配置文件中查询一个匹配的 bean。如果找到的话，就装配这个属性，如果没找到的话就报错。

3.	byType：该选项可以根据 bean 类型设置依赖关系。当向一个 bean 中自动装配一个属性时，容器将根据 bean 的类型自动在在配置文件中查询一个匹配的 bean。如果找到的话，就装配这个属性， 如果没找到的话就报错。

4.	constructor：造器的自动装配和 byType 模式类似，但是仅仅适用于与有构造器相同参数的
bean，如果在容器中没有找到与构造器参数类型一致的 bean，那么将会抛出异常。

5.	autodetect：该模式自动探测使用构造器自动装配或者 byType 自动装配。首先，首先会尝试找合适的带参数的构造器，如果找到的话就是用构造器自动装配，如果在 bean 内部没有找到相应的构造器或者是无参构造器，容器就会自动选择 byTpe 的自动装配方式。
18、如何开启基于注解的自动装配？
要使用 @Autowired，需要注册 AutowiredAnnotationBeanPostProcessor，可以有以下两种方式来实现：
1、引入配置文件中的<bean>下引入 <context:annotation-config>
<beans>     
    <context:annotation-config />     
</beans>    





2、在 bean 配置文件中直接引入 AutowiredAnnotationBeanPostProcessor
<beans>     
    <bean class="org.springframework.beans.factory.annotation.AutowiredAnnotati onBeanPostProcessor"/>     
</beans> 
 
### 45. 请举例解释@Required 注解？
在产品级别的应用中，IoC 容器可能声明了数十万了 bean，bean 与 bean 之间有着复杂的依赖关系。设值注解方法的短板之一就是验证所有的属性是否被注解是一项十分困难的操作。可以通过在
<bean>中设置“dependency-check”来解决这个问题。
在应用程序的生命周期中，你可能不大愿意花时间在验证所有 bean 的属性是否按照上下文文件正确配置。或者你宁可验证某个 bean 的特定属性是否被正确的设置。即使是用“dependency- check”属性也不能很好的解决这个问题，在这种情况下，你需要使用@Required 注解。
需要用如下的方式使用来标明 bean 的设值方法。


 
public class EmployeeFactoryBean extends AbstractFactoryBean<Object>{     
    private String designation;     
    public String getDesignation() {     
        return designation;     
    }     
    @Required     
    public void setDesignation(String designation) {     
        this.designation = designation;     
    }     
    //more code here     
}     
 





RequiredAnnotationBeanPostProcessor 是 Spring 中的后置处理用来验证被@Required 注解的 bean 属性是否被正确的设置了。在使用RequiredAnnotationBeanPostProcesso 来验证 bean 属性之前，首先要在 IoC 容器中对其进行注册：






 
但是如果没有属性被用 @Required 注解过的话，后置处理器会抛出一个
BeanInitializationException 异常。


### 46. 请举例解释@Autowired 注解？

@Autowired 注解对自动装配何时何处被实现提供了更多细粒度的控制。@Autowired 注解可
以像@Required 注解、构造器一样被用于在 bean 的设值方法上自动装配 bean
的属性，一个参数或者带有任意名称或带有多个参数的方法。
比如，可以在设值方法上使用@Autowired 注解来替代配置文件中的 <property>元
素。当 Spring 容器在 setter 方法上找到@Autowired 注解时，会尝试用 byType
自动装配。
当然我们也可以在构造方法上使用@Autowired 注解。带有@Autowired 注解的构造方法意味着在创建一个 bean 时将会被自动装配，即便在配置文件中使用<constructor-arg> 元素。
 

下面是没有构造参数的配置方式：


 
 





### 47. 请举例说明@Qualifier 注解？

@Qualifier 注解意味着可以在被标注 bean 的字段上可以自动装配。Qualifier 注解可以用来取消 Spring 不能取消的 bean 应用。
下面的示例将会在 Customer 的 person 属性中自动装配 person 的值。



下面我们要在配置文件中来配置 Person 类。


 
Spring 会知道要自动装配哪个 person bean 么？不会的，但是运行上面的示例时，会抛出下面的异常：


Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException:     
    No unique bean of type [com.howtodoinjava.common.Person] is defined:     
        expected single matching bean but found 2: [personA, personB]     





要解决上面的问题，需要使用 @Quanlifier 注解来告诉 Spring 容器要装配哪个 bean：







### 48. 构造方法注入和设值注入有什么区别？
请注意以下明显的区别：

1.	在设值注入方法支持大部分的依赖注入，如果我们仅需 要注入 int、string 和 long 型的变量，我们不要用设值的方法注入。对于基本类型，如果我们没有注入的话，可以为基本类型设置默认值。在构造方法 注入不支持大部分的依赖注入，因为在调用构造方法中必须传入正确的构造参数，否则的话为报错。

2.	设值注入不会重写构造方法的值。如果我们对同一个变量同时使用了构造方法注入又使用了设置方法注入的话，那么构造方法将不能覆盖由设值方法注入的值。很明显，因为构造方法尽在对象被创建时调用。

3.	在使用设值注入时有可能还不能保证某种依赖是否已经被注入，也就是说这时对象的依赖关系有可能是不完整的。而在另一种情况下，构造器注入则不允许生成依赖关系不完整的对象。

4.	在设值注入时如果对象 A 和对象 B 互相依赖，在创建对象 A 时 Spring 会抛出sObjectCurrentlyInCreationException 异常，因为在 B 对象被创建之前 A 对象是不能被创建的，反之亦然。所以 Spring 用设值注入的方法解决了循环依赖的问题，因对象的设值方法是在对象被创建之前被调用的。
23、Spring 框架中有哪些不同类型的事件？
 
Spring 的 ApplicationContext 提供了支持事件和代码中监听器的功能。
我们可以创建 bean 用来监听在 ApplicationContext 中发布的事件。ApplicationEvent 类和在 ApplicationContext 接口中处理的事件，如果一个 bean 实现了ApplicationListener 接口，当一个 ApplicationEvent 被发布以后，bean 会自动被通知。

public class AllApplicationEventListener implements ApplicationListener 
< ApplicationEvent >{     
    @Override     
    public void onApplicationEvent(ApplicationEvent applicationEvent)     
    {     
        //process event     
    }     
}     








Spring 提供了以下 5 中标准的事件：
1.	上下文更新事件（ContextRefreshedEvent）：该事件会在 ApplicationContext 被初始化或者更新时发布。也可以在调用 ConfigurableApplicationContext 接口中的 refresh()方法时被触发。

2.	上下文开始事件（ContextStartedEvent）：当容器调用 ConfigurableApplicationContext 的
Start()方法开始/重新开始容器时触发该事件。

3.	上下文停止事件（ContextStoppedEvent）：当容器调用 ConfigurableApplicationContext 的
Stop()方法停止容器时触发该事件。

4.	上下文关闭事件（ContextClosedEvent）：当 ApplicationContext 被关闭时触发该事件。容器被关闭时，其管理的所有单例 Bean 都被销毁。

5.	请求处理事件（RequestHandledEvent）：在 Web 应用中，当一个 http 请求（request）结束触发该事件。

除了上面介绍的事件以外，还可以通过扩展 ApplicationEvent 类来开发自定义的事件。
public class CustomApplicationEvent extends ApplicationEvent{     
    public CustomApplicationEvent ( Object source, final String msg ){     
        super(source);     
        System.out.println("Created a Custom event");     
    }     
}     
 
 


为了监听这个事件，还需要创建一个监听器：



之后通过 applicationContext 接口的 publishEvent()方法来发布自定义事件。
 



### 49. FileSystemResource 和 ClassPathResource 有何区别？
在 FileSystemResource 中需要给出 spring-config.xml 文件在你项目中的相对路径或者绝对路径。在 ClassPathResource 中 spring 会在 ClassPath 中自动搜寻配置文件，所以要把ClassPathResource 文件放在 ClassPath 下。
如果将 spring-config.xml 保存在了 src 文件夹下的话，只需给出配置文件的名称即可，因为src 文件夹是默认。
简而言之，ClassPathResource 在环境变量中读取配置文件，FileSystemResource 在配置文件中读取配置文件。
### 50 .Spring 框架中都用到了哪些设计模式？
Spring 框架中使用到了大量的设计模式，下面列举了比较有代表性的：
o	代理模式—在 AOP 和 remoting 中被用的比较多。

o	单例模式—在 spring 配置文件中定义的 bean 默认为单例模式。
 
o	模板方法—用来解决代码重复的问题。比如. RestTemplate, JmsTemplate, JpaTempl ate。
o	前端控制器—Spring 提供了 DispatcherServlet 来对请求进行分发。
o	视图帮助(View Helper )—Spring 提供了一系列的 JSP 标签，高效宏来辅助将分散的代码整合在视图里。

o	依赖注入—贯穿于 BeanFactory / ApplicationContext 接口的核心理念。
o	工厂模式—BeanFactory 用来创建对象的实例





1.	开发中主要使用 Spring 的什么技术 ?
①. IOC 容器管理各层的组件
②. 使用 AOP 配置声明式事务
③. 整合其他框架.


2.	简 述 AOP 和 IOC 概 念 AOP:
Aspect Oriented Program, 面向(方面)切面的编程;Filter(过滤器) 也是一种 AOP. AOP 是一种新的方法论, 是对传统 OOP(Object-Oriented Programming, 面向对象编程) 的补充. AOP 的主要编程对象是切面(aspect), 而切面模块化横切关注点.可以举例通过事务说明.


IOC: Invert Of Control, 控制反转. 也成为 DI(依赖注入)其思想是反转 资源获取的方向. 传统的资源查找方式要求组件向容器发起请求查找资源.作为 回应, 容器适时的返回资源. 而应用了IOC 之后, 则是容器主动地将资源推送 给它所管理的组件,组件所要做的仅是选择一种合适的方式来接受资源. 这种行 为也被称为查找的被动形式

3.	在 Spring 中如何配置 Bean ?
Bean 的配置方式: 通过全类名（反射）、通过工厂方法（静态工厂方法 & 实 例工厂方法）、
FactoryBean


4.	IOC 容器对 Bean 的生命周期:
①. 通过构造器或工厂方法创建 Bean 实例
②. 为 Bean 的属性设置值和对其他 Bean 的引用
③ . 将 Bean 实 例 传 递 给 Bean 后 置 处 理 器 的 postProcessBeforeInitialization 方法
④. 调用 Bean 的初始化方法(init-method)
 
⑤ . 将 Bean 实 例 传 递 给 Bean 后 置 处 理 器 的 postProcessAfterInitialization 方 法
⑦. Bean 可以使用了
⑧. 当容器关闭时, 调用 Bean 的销毁方法(destroy-method)
