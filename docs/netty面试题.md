### 1、谈谈你对natty的认识

1. Netty 是⼀个 基于 NIO 的 client-server(客户端服务器)框架，使⽤它可以快速简单地开发⽹
  络应⽤程序。

2. 它极⼤地简化并优化了 TCP 和 UDP 套接字服务器等⽹络编程,并且性能以及安全性等很多
  ⽅⾯甚⾄都要更好。

3. ⽀持多种协议 如 FTP，SMTP，HTTP 以及各种⼆进制和基于⽂本的传统协议。

  **用到netty的常用开源框架： Dubbo、RocketMQ、Elasticsearch、gRPC等**


### 2、netty有哪些应用场景？

    1. 作为 RPC 框架的⽹络通信⼯具 ： 我们在分布式系统中，不同服务节点之间经常需要相互调
    ⽤，这个时候就需要 RPC 框架了。不同服务节点之间的通信是如何做的呢？可以使⽤ Netty
    来做。⽐如我调⽤另外⼀个节点的⽅法的话，⾄少是要让对⽅知道我调⽤的是哪个类中的哪
    个⽅法以及相关参数吧！
    2. 实现⼀个⾃⼰的 HTTP 服务器 ：通过 Netty 我们可以⾃⼰实现⼀个简单的 HTTP 服务器，
    这个⼤家应该不陌⽣。说到 HTTP 服务器的话，作为 Java 后端开发，我们⼀般使⽤
    Tomcat ⽐᫾多。⼀个最基本的 HTTP 服务器可要以处理常⻅的 HTTP Method 的请求，⽐
    如 POST 请求、GET 请求等等。

### 3、用netty有哪些优点？

统⼀的 API，⽀持多种传输类型，阻塞和⾮阻塞的。
简单⽽强⼤的线程模型。
⾃带编解码器解决 TCP 粘包/拆包问题。
⾃带各种协议栈。
真正的⽆连接数据包套接字⽀持。
⽐直接使⽤ Java 核⼼ API 有更⾼的吞吐量、更低的延迟、更低的资源消耗和更少的内存复
制。
安全性不错，有完整的 SSL/TLS 以及 StartTLS ⽀持。
社区活跃
成熟稳定，经历了⼤型项⽬的使⽤和考验，⽽且很多开源项⽬都使⽤到了 Netty， ⽐如我们
经常接触的 Dubbo、RocketMQ 等等。

### 4、netty有哪些核心组件？





### 5、聊聊：JDK原生NIO程序的问题？

JDK原生也有一套网络应用程序API，但是存在一系列问题，主要如下：

+   NIO的类库和API繁杂，使用麻烦，你需要熟练掌握Selector、ServerSocketChannel、SocketChannel、ByteBuffer等

+   需要具备其它的额外技能做铺垫，例如熟悉Java多线程编程，因为NIO编程涉及到Reactor模式，你必须对多线程和网路编程非常熟悉，才能编写出高质量的NIO程序

+   可靠性能力补齐，开发工作量和难度都非常大。

    例如客户端面临断连重连、网络闪断、半包读写、失败缓存、网络拥塞和异常码流的处理等等，NIO编程的特点是功能开发相对容易，但是可靠性能力补齐工作量和难度都非常大

+   JDK NIO的BUG，例如臭名昭著的select bug，它会导致Selector空轮询，最终导致CPU 100%。

    官方声称在JDK1.6版本的update18修复了该问题，但是直到JDK1.7版本该问题仍旧存在，只不过该bug发生概率降低了一些而已，它并没有被根本解决


### 6、Netty 的优势有哪些？

+   使用简单：封装了 NIO 的很多细节，使用更简单。
+   功能强大：预置了多种编解码功能，支持多种主流协议。
+   定制能力强：可以通过 ChannelHandler 对通信框架进行灵活地扩展。
+   性能高：通过与其他业界主流的 NIO 框架对比，Netty 的综合性能最优。
+   稳定：Netty 修复了已经发现的所有 NIO 的 bug，让开发人员可以专注于业务本身。
+   社区活跃：Netty 是活跃的开源项目，版本迭代周期短，bug 修复速度快。

### 7、Netty 的应用场景有哪些？

典型的应用有：

+   阿里分布式服务框架 Dubbo，默认使用 Netty 作为基础通信组件，

+   还有 RocketMQ 也是使用 Netty 作为通讯的基础。


Netty常见的使用场景如下：

+   互联网行业 在分布式系统中，各个节点之间需要远程服务调用，高性能的RPC框架必不可少，Netty作为异步高新能的通信框架,往往作为基础通信组件被这些RPC框架使用。 典型的应用有：阿里分布式服务框架Dubbo的RPC框架使用Dubbo协议进行节点间通信，Dubbo协议默认使用Netty作为基础通信组件，用于实现各进程节点之间的内部通信。
+   游戏行业 无论是手游服务端还是大型的网络游戏，Java语言得到了越来越广泛的应用。Netty作为高性能的基础通信组件，它本身提供了TCP/UDP和HTTP协议栈。 非常方便定制和开发私有协议栈，账号登录服务器，地图服务器之间可以方便的通过Netty进行高性能的通信
+   大数据领域 经典的Hadoop的高性能通信和序列化组件Avro的RPC框架，默认采用Netty进行跨界点通信，它的Netty Service基于Netty框架二次封装实现

### 8、Netty的特点

Netty的对JDK自带的NIO的API进行封装，解决上述问题，主要特点有：

+   设计优雅 适用于各种传输类型的统一API - 阻塞和非阻塞Socket 基于灵活且可扩展的事件模型，可以清晰地分离关注点 高度可定制的线程模型 - 单线程，一个或多个线程池 真正的无连接数据报套接字支持（自3.1起）

+   高性能 、高吞吐、低延迟、低消耗

+   最小化不必要的内存复制

+   安全 完整的SSL / TLS和StartTLS支持

+   高并发：Netty 是一款基于 NIO（Nonblocking IO，非阻塞IO）开发的网络通信框架，对比于 BIO（Blocking I/O，阻塞IO），他的并发性能得到了很大提高。

+   传输快：Netty 的传输依赖于零拷贝特性，尽量减少不必要的内存拷贝，实现了更高效率的传输。

+   封装好：Netty 封装了 NIO 操作的很多细节，提供了易于使用调用接口。

+   社区活跃，不断更新 社区活跃，版本迭代周期短，发现的BUG可以被及时修复，同时，更多的新功能会被加入

+   使用方便 详细记录的Javadoc，用户指南和示例 没有其他依赖项，JDK 5（Netty 3.x）或6（Netty 4.x）就足够了


### 9、Netty 高性能表现在哪些方面？

+   IO 线程模型：通过多线程Reactor反应器模式，在应用层实现异步非阻塞（异步事件驱动）架构，用最少的资源做更多的事。
+   内存零拷贝：尽量减少不必要的内存拷贝，实现了更高效率的传输。
+   内存池设计：申请的内存可以重用，主要指直接内存。内部实现是用一颗二叉查找树管理内存分配情况。 （**具体请参考尼恩稍后的手写内存池**）
+   对象池设计：Java对象可以重用，主要指Minior GC非常频繁的对象，如ByteBuffer。并且，**对象池使用无锁架构**，性能非常高。 （**具体请参考尼恩稍后的手写对象池**）
+   mpsc无锁编程：串形化处理读写, 避免使用锁带来的性能开销。
+   高性能序列化协议：支持 protobuf 等高性能序列化协议。

### 10、聊聊：NIO的组成？

Buffer：与Channel进行交互，数据是从Channel读入缓冲区，从缓冲区写入Channel中的

flip方法 ： 反转此缓冲区，将position给limit，然后将position置为0，其实就是切换读写模式

clear方法 ：清除此缓冲区，将position置为0，把capacity的值给limit。

rewind方法 ： 重绕此缓冲区，将position置为0

DirectByteBuffer可减少一次系统空间到用户空间的拷贝。但Buffer创建和销毁的成本更高，不可控，通常会用内存池来提高性能。直接缓冲区主要分配给那些易受基础系统的本机I/O 操作影响的大型、持久的缓冲区。如果数据量比较小的中小应用情况下，可以考虑使用heapBuffer，由JVM进行管理。

Channel：表示 IO 源与目标打开的连接，是双向的，但不能直接访问数据，只能与Buffer 进行交互。通过源码可知，FileChannel的read方法和write方法都导致数据复制了两次！

Selector可使一个单独的线程管理多个Channel，open方法可创建Selector，register方法向多路复用器器注册通道，可以监听的事件类型：读、写、连接、accept。注册事件后会产生一个SelectionKey：它表示SelectableChannel 和Selector 之间的注册关系，wakeup方法：使尚未返回的第一个选择操作立即返回，唤醒的

原因是：注册了新的channel或者事件；channel关闭，取消注册；优先级更高的事件触发（如定时器事件），希望及时处理。

Selector在Linux的实现类是EPollSelectorImpl，委托给EPollArrayWrapper实现，其中三个native方法是对epoll的封装，而EPollSelectorImpl. implRegister方法，通过调用epoll\_ctl向epoll实例中注册事件，还将注册的文件描述符(fd)与SelectionKey的对应关系添加到fdToKey中，这个map维护了文件描述符与SelectionKey的映射。

fdToKey有时会变得非常大，因为注册到Selector上的Channel非常多（百万连接）；过期或失效的Channel没有及时关闭。fdToKey总是串行读取的，而读取是在select方法中进行的，该方法是非线程安全的。

Pipe：两个线程之间的单向数据连接，数据会被写到sink通道，从source通道读取

NIO的服务端建立过程：Selector.open()：打开一个Selector；ServerSocketChannel.open()：创建服务端的Channel；bind()：绑定到某个端口上。并配置非阻塞模式；register()：注册Channel和关注的事件到Selector上；select()轮询拿到已经就绪的事件

### 11、聊聊：BIO、NIO和AIO的区别？

BIO：一个连接一个线程，客户端有连接请求时服务器端就需要启动一个线程进行处理。线程开销大。  
伪异步IO：将请求连接放入线程池，一对多，但线程还是很宝贵的资源。

NIO：一个请求一个线程，但客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。

AIO：一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理，

BIO是面向流的，NIO是面向缓冲区的；

BIO的各种流是阻塞的。而NIO是非阻塞的；

BIO的Stream是单向的，而NIO的channel是双向的。

NIO的特点：事件驱动模型、单线程处理多任务、非阻塞I/O，I/O读写不再阻塞，而是返回0、基于block的传输比基于流的传输更高效、更高级的IO函数zero-copy、IO多路复用大大提高了Java网络应用的可伸缩性和实用性。基于Reactor线程模型。

在Reactor模式中，事件分发器等待某个事件或者可应用或个操作的状态发生，事件分发器就把这个事件传给事先注册的事件处理函数或者回调函数，由后者来做实际的读写操作。如在Reactor中实现读：注册读就绪事件和相应的事件处理器、事件分发器等待事件、事件到来，激活分发器，分发器调用事件对应的处理器、事件处理器完成实际的读操作，处理读到的数据，注册新的事件，然后返还控制权。

### 12、Netty 和 Tomcat 的区别？

+   作用不同：Tomcat 是 Servlet 容器，可以视为 Web 服务器，而 Netty 是异步事件驱动的网络应用程序框架和工具用于简化网络编程，例如TCP和UDP套接字服务器。
+   协议不同：Tomcat 是基于 http 协议的 Web 服务器，而 Netty 能通过编程自定义各种协议，因为 Netty 本身自己能编码/解码字节流，所有 Netty 可以实现，HTTP 服务器、FTP 服务器、UDP 服务器、RPC 服务器、WebSocket 服务器、Redis 的 Proxy 服务器、MySQL 的 Proxy 服务器等等。

### 13、聊聊：Netty是怎么实现高性能设计的？

Netty作为高性能IO组件的扛鼎制作，

高性能设计的核心： 巧妙的 结合 高性能IO模型 和 线程模型 ，相得益彰，达到了 高性能 、高吞吐、低延迟、低消耗的目标

其I/O模型 高性能epoll/select 模型

其 线程模型为 多线程 reactor 反应器模型

I/O模型 决定如何收发数据，

线程模型 决定如何处理数据

相得益彰，在应用层达到了异步IO的效果。

### 14、聊聊：I/O模型

用什么样的通道将数据发送给对方，BIO、NIO或者AIO，I/O模型在很大程度上决定了框架的性能

答案请参考[《Java高并发核心编程 卷1 》](https://www.cnblogs.com/crazymakercircle/p/14493539.html)

书中，对io模型介绍得非常系统，并且不断完善

#### 1、阻塞I/O

传统阻塞型I/O(BIO)可以用下图表示：

![Blocking I/O](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJjZmI3MGMxMTE?x-oss-process=image/format,png)

**特点**

+   每个请求都需要独立的线程完成数据read，业务处理，数据write的完整操作

**问题**

+   当并发数较大时，需要创建大量线程来处理连接，系统资源占用较大
+   连接建立后，如果当前线程暂时没有数据可读，则线程就阻塞在read操作上，造成线程资源浪费

#### 2、I/O复用模型

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJjZmJhNTNjMGE?x-oss-process=image/format,png)

在I/O复用模型中，会用到select，这个函数也会使进程阻塞，但是和阻塞I/O所不同的的，这两个函数可以同时阻塞多个I/O操作，而且可以同时对多个读操作，多个写操作的I/O函数进行检测，直到有数据可读或可写时，才真正调用I/O操作函数

Netty的非阻塞I/O的实现关键是基于I/O复用模型，这里用Selector对象表示：

![Nonblocking I/O](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJjZmJhMzIxNjk?x-oss-process=image/format,png)

Netty的IO线程NioEventLoop由于聚合了多路复用器Selector，可以同时并发处理成百上千个客户端连接。当线程从某客户端Socket通道进行读写数据时，若没有数据可用时，该线程可以进行其他任务。线程通常将非阻塞 IO 的空闲时间用于在其他通道上执行 IO 操作，所以单独的线程可以管理多个输入和输出通道。

由于读写操作都是非阻塞的，这就可以充分提升IO线程的运行效率，避免由于频繁I/O阻塞导致的线程挂起，一个I/O线程可以并发处理N个客户端连接和读写操作，这从根本上解决了传统同步阻塞I/O一连接一线程模型，架构的性能、弹性伸缩能力和可靠性都得到了极大的提升。

#### 3、基于buffer

传统的I/O是面向字节流或字符流的，以流式的方式顺序地从一个Stream 中读取一个或多个字节, 因此也就不能随意改变读取指针的位置。

在NIO中, 抛弃了传统的 I/O流, 而是引入了Channel和Buffer的概念. 在NIO中, 只能从Channel中读取数据到Buffer中或将数据 Buffer 中写入到 Channel。

基于buffer操作不像传统IO的顺序操作, NIO 中可以随意地读取任意位置的数据

### 15、聊聊：AIO 是什么？

1、JDK7引入了Asynchronous I/O，即AIO。在进行I/O编程中，常用到两种模式：Reactor（反应器模式）和Proactor。Java的NIO就是Reactor，当有事件触发时，服务端得到通知，进行相应的处理。

2、AIO即NIO2.0，叫做异步不阻塞的IO。AIO引入异步通道的概念，采用了Proactor模式，简化了程序编写，有效的请求才启动线程，它的特点是先由操作系统完成后才通知服务端程序启动线程去处理，一般适用于连接数较多且连接时间较长的应用。


### 16、聊聊：NIO和BIO到底有什么区别？有什么关系？

1.  NIO是以块的方式处理数据，BIO是以字节流或者字符流的形式去处理数据。
2.  NIO是通过缓存区和通道的方式处理数据，BIO是通过InputStream和OutputStream流的方式处理数据。
3.  NIO的通道是双向的，BIO流的方向只能是单向的。
4.  NIO采用的多路复用的同步非阻塞IO模型，BIO采用的是普通的同步阻塞IO模型。
5.  NIO的效率比BIO要高，NIO适用于网络IO，BIO适用于文件IO。

### 17、聊聊：NIO是如何实现同步非阻塞的？

一个线程 Thread 使用一个选择器Selector监听多个通道 Channel 上的IO事件，从而让一个线程就可以处理多个IO事件。通过配置监听的通道Channel为非阻塞，那么当Channel上的IO事件还未到达时，线程会在select方法被挂起，让出CPU资源。直到监听到Channel有IO事件发生时，才会进行相应的响应和处理。

Selector能够检测多个注册的通道上是否有IO事件发生(注意:多个 Channel 以事件的方式可以注册到同一个Selector)，如果有事件发生，便获取事件然后针对每个事件进行相应的处理。这样就可以只用一个单线程去管理多个通道，也就是管理多个连接和请求。

Selector只有在通道上有真正的IO事件发生时，才会进行相应的处理，这就不必为每个连接都创建一个线程，避免线程资源的浪费和多线程之间的上下文切换导致的开销。

### 18、聊聊：BIO和NIO应用场景

1、**BIO** 方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择。

2、**NIO** 方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，弹幕系统，服务器间通讯等。JDK1.4 开始支持。

### 19、聊聊：阻塞/非阻塞区别

（1）同步阻塞：到理发店理发，就一直等理发师，直到轮到自己。
（2）同步非阻塞：到理发店理发，发现前面有其他人理发，给理发师说下，先干其他事情，一会儿过来看是否轮到自己。
（3）异步非阻塞：给理发师打电话，让理发师上门服务，自己干其他事情，理发师自己来家给你理发。

### 20、聊聊：同步/异步区别

同步与异步的区别在于，异步基于通知，当程序执行完毕后后，会有一个通知的机制来告知你程序执行完毕；而同步则没有，只能通过自己调用API去查询程序是否已经执行完毕。

### 21、聊聊：select、poll和epoll的区别

#### 消息传递方式：

select：内核需要将消息传递到用户空间，需要内核的拷贝动作；

poll：同上；

epoll：通过内核和用户空间共享一块内存来实现，性能较高；

#### 文件句柄剧增后带来的IO效率问题：

select：因为每次调用都会对连接进行线性遍历，所以随着FD剧增后会造成遍历速度的“线性下降”的性能问题；

poll：同上；

epoll：由于epoll是根据每个FD上的callable函数来实现的，只有活跃的socket才会主动调用callback，所以在活跃socket较少的情况下，使用epoll不会对性能产生线性下降的问题，如果所有socket都很活跃的情况下，可能会有性能问题；

#### 支持一个进程所能打开的最大连接数：

select：单个进程所能打开的最大连接数，是由FD\_SETSIZE宏定义的，其大小是32个整数大小（在32位的机器上，大小是32*32,64位机器上FD\_SETSIZE=32*64），我们可以对其进行修改，然后重新编译内核，但是性能无法保证，需要做进一步测试；

poll：本质上与select没什么区别，但是他没有最大连接数限制，他是基于链表来存储的；

epoll：虽然连接数有上线，但是很大，1G内存的机器上可以打开10W左右的连接；

### 25、聊聊: 主要的IO线程模型有哪些?

数据报如何读取？读取之后的编解码在哪个线程进行，编解码后的消息如何派发，线程模型的不同，对性能的影响也非常大。

### Connection Per Thread（一个线程处理一个连接）线程模式

在Java的OIO编程中，最原始的网络服务器程序，一般是用一个while循环，不断地监听端口是否有新的连接。

如果有，那么就调用一个处理函数来完成传输处理，示例代码如下：

```auto
while(true){

  socket = accept(); //阻塞，接收连接

  handle(socket) ;  //读取数据、业务处理、写入结果

} 
```

这种方法的最大问题是：如果前一个网络连接的handle（socket）没有处理完，那么后面的新连接没法被服务端接收，于是后面的请求就会被阻塞住，这样就导致服务器的吞吐量太低。

这对于服务器来说，这是一个严重的问题。

为了解决这个严重的连接阻塞问题，出现了一个极为经典模式：Connection Per Thread（一个线程处理一个连接）模式。示例代码如下：

```auto

package com.crazymakercircle.iodemo.OIO;
//...省略import导入的Java类
class ConnectionPerThread implements Runnable {
    public void run() {
        try {
            //服务器监听socket
            ServerSocketserverSocket =
                    new ServerSocket(NioDemoConfig.SOCKET_SERVER_PORT);
            while (!Thread.interrupted()) {
                Socket socket = serverSocket.accept();
                //接收一个连接后，为socket连接，新建一个专属的处理器对象
                Handler handler = new Handler(socket);
                //创建新线程，专门负责一个连接的处理
                new Thread(handler).start();
            }

        } catch (IOException ex) { /* 处理异常 */ }
    }
    //处理器，这里将内容回显到客户端
    static class Handler implements Runnable {
        final Socket socket;
        Handler(Socket s) {
            socket = s;
        }
        public void run() {
            while (true) {
                try {
                    byte[] input = new byte[1024];
                    /* 读取数据 */
                    socket.getInputStream().read(input);
                    /* 处理业务逻辑，获取处理结果*/
                    byte[] output =null;
                    /* 写入结果 */
                    socket.getOutputStream().write(output);
                } catch (IOException ex) { /*处理异常*/ }
            }
        }
    }
}


```

以上示例代码中，对于每一个新的网络连接都分配给一个线程。每个线程都独自处理自己负责的socket连接的输入和输出。当然，服务器的监听线程也是独立的，任何的socket连接的输入和输出处理，不会阻塞到后面新socket连接的监听和建立，这样，服务器的吞吐量就得到了提升。早期版本的Tomcat服务器，就是这样实现的。

Connection Per Thread模式（一个线程处理一个连接）的优点是：解决了前面的新连接被严重阻塞的问题，在一定程度上，较大的提高了服务器的吞吐量。

Connection Per Thread模式的缺点是：对应于大量的连接，需要耗费大量的线程资源，对线程资源要求太高。在系统中，线程是比较昂贵的系统资源。如果线程的数量太多，系统无法承受。而且，线程的反复创建、销毁、线程的切换也需要代价。因此，在高并发的应用场景下，多线程OIO的缺陷是致命的。

新的问题来了：如何减少线程数量，比如说让一个线程同时负责处理多个socket连接的输入和输出，行不行呢？

看上去，没有什么不可以。但是，实际上作用不大。为什么呢？传统OIO编程中每一次socket传输的IO读写处理，都是阻塞的。在同一时刻，一个线程里只能处理一个socket的读写操作，前一个socket操作被阻塞了，其他连接的IO操作同样无法被并行处理。所以在OIO中，即使是一个线程同时负责处理多个socket连接的输入和输出，同一时刻，该线程也只能处理一个连接的IO操作。

如何解决Connection Per Thread模式的巨大缺陷呢？一个有效途径是：使用Reactor反应器模式。用反应器模式对线程的数量进行控制，做到一个线程处理大量的连接。

### Reactor线程模型

Reactor是反应堆/反应器的意思，Reactor模型，是指通过一个或多个输入同时传递给服务处理器的服务请求的**事件驱动处理模式**。 服务端程序处理传入多路请求，并将它们同步分派给请求对应的处理线程，Reactor模式也叫Dispatcher模式，即I/O多了复用统一监听事件，收到事件后分发(Dispatch给某进程)，是编写高性能网络服务器的必备技术之一。

Reactor模型中有2个关键组成：

+   Reactor Reactor在一个单独的线程中运行，负责监听和分发事件，分发给适当的处理程序来对IO事件做出反应。 它就像公司的电话接线员，它接听来自客户的电话并将线路转移到适当的联系人
+   Handlers 处理程序执行I/O事件要完成的实际事件，类似于客户想要与之交谈的公司中的实际官员。Reactor通过调度适当的处理程序来响应I/O事件，处理程序执行非阻塞操作

![Reactor模型](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJkYzY1NGQ2ZGM?x-oss-process=image/format,png)

取决于Reactor的数量和Hanndler线程数量的不同，Reactor模型有3个变种

+   单Reactor单线程
+   单Reactor多线程
+   主从Reactor多线程

可以这样理解，Reactor就是一个执行while (true) { selector.select(); …}循环的线程，会源源不断的产生新的事件，称作反应堆很贴切。

### Netty线程模型

Netty主要**基于主从Reactors多线程模型**（如下图）做了一定的修改，其中主从Reactor多线程模型有多个Reactor：MainReactor和SubReactor：

+   MainReactor负责客户端的连接请求，并将请求转交给SubReactor
+   SubReactor负责相应通道的IO读写请求
+   非IO请求（具体逻辑处理）的任务则会直接写入队列，等待worker threads进行处理

这里引用Doug Lee大神的Reactor介绍：[Scalable IO in Java](http://gee.cs.oswego.edu/dl/cpjslides/nio.pdf)里面关于主从Reactor多线程模型的图

![主从Rreactor多线程模型](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJkYzY5OGRkZDY?x-oss-process=image/format,png)

特别说明的是： 虽然Netty的线程模型基于主从Reactor多线程，借用了MainReactor和SubReactor的结构，但是实际实现上，SubReactor和Worker线程在同一个线程池中：

```java
EventLoopGroup bossGroup = new NioEventLoopGroup();
EventLoopGroup workerGroup = new NioEventLoopGroup();
ServerBootstrap server = new ServerBootstrap();
server.group(bossGroup, workerGroup)
 .channel(NioServerSocketChannel.class)


```

上面代码中的bossGroup 和workerGroup是Bootstrap构造方法中传入的两个对象，这两个group均是线程池

+   bossGroup线程池则只是在bind某个端口后，获得其中一个线程作为MainReactor，专门处理端口的accept事件，**每个端口对应一个boss线程**
+   workerGroup线程池会被各个SubReactor和worker线程充分利用

### 异步处理

异步的概念和同步相对。当一个异步过程调用发出后，调用者不能立刻得到结果。实际处理这个调用的部件在完成后，通过状态、通知和回调来通知调用者。

Netty中的I/O操作是异步的，包括bind、write、connect等操作会简单的返回一个ChannelFuture，调用者并不能立刻获得结果，通过Future-Listener机制，用户可以方便的主动获取或者通过通知机制获得IO操作结果。

当future对象刚刚创建时，处于非完成状态，调用者可以通过返回的ChannelFuture来获取操作执行的状态，注册监听函数来执行完成后的操，常见有如下操作：

+   通过isDone方法来判断当前操作是否完成
+   通过isSuccess方法来判断已完成的当前操作是否成功
+   通过getCause方法来获取已完成的当前操作失败的原因
+   通过isCancelled方法来判断已完成的当前操作是否被取消
+   通过addListener方法来注册监听器，当操作已完成(isDone方法返回完成)，将会通知指定的监听器；如果future对象已完成，则理解通知指定的监听器

例如下面的的代码中绑定端口是异步操作，当绑定操作处理完，将会调用相应的监听器处理逻辑

```java
    serverBootstrap.bind(port).addListener(future -> {
        if (future.isSuccess()) {
            System.out.println(new Date() + ": 端口[" + port + "]绑定成功!");
        } else {
            System.err.println("端口[" + port + "]绑定失败!");
        }
    });


```

相比传统阻塞I/O，执行I/O操作后线程会被阻塞住, 直到操作完成；异步处理的好处是不会造成线程阻塞，线程在I/O操作期间可以执行别的程序，在高并发情形下会更稳定和更高的吞吐量。

### 26、Netty架构设计

前面介绍完Netty相关一些理论介绍，下面从功能特性、模块组件、运作过程来介绍Netty的架构设计

### 功能特性

![Netty功能特性图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJkYzg2MTRjOGY?x-oss-process=image/format,png)

+   传输服务 支持BIO和NIO
+   容器集成 支持OSGI、JBossMC、Spring、Guice容器
+   协议支持 HTTP、Protobuf、二进制、文本、WebSocket等一系列常见协议都支持。 还支持通过实行编码解码逻辑来实现自定义协议
+   Core核心 可扩展事件模型、通用通信API、支持零拷贝的ByteBuf缓冲对象

### 模块组件

#### Bootstrap、ServerBootstrap

Bootstrap意思是引导，一个Netty应用通常由一个Bootstrap开始，主要作用是配置整个Netty程序，串联各个组件，Netty中Bootstrap类是客户端程序的启动引导类，ServerBootstrap是服务端启动引导类。

#### Future、ChannelFuture

正如前面介绍，在Netty中所有的IO操作都是异步的，不能立刻得知消息是否被正确处理，但是可以过一会等它执行完成或者直接注册一个监听，具体的实现就是通过Future和ChannelFutures，他们可以注册一个监听，当操作执行成功或失败时监听会自动触发注册的监听事件。

#### Channel

Netty网络通信的组件，能够用于执行网络I/O操作。 Channel为用户提供：

+   当前网络连接的通道的状态（例如是否打开？是否已连接？）
+   网络连接的配置参数 （例如接收缓冲区大小）
+   提供异步的网络I/O操作(如建立连接，读写，绑定端口)，异步调用意味着任何I / O调用都将立即返回，并且不保证在调用结束时所请求的I / O操作已完成。调用立即返回一个ChannelFuture实例，通过注册监听器到ChannelFuture上，可以I / O操作成功、失败或取消时回调通知调用方。
+   支持关联I/O操作与对应的处理程序

不同协议、不同的阻塞类型的连接都有不同的 Channel 类型与之对应，下面是一些常用的 Channel 类型

+   NioSocketChannel，异步的客户端 TCP Socket 连接
+   NioServerSocketChannel，异步的服务器端 TCP Socket 连接
+   NioDatagramChannel，异步的 UDP 连接
+   NioSctpChannel，异步的客户端 Sctp 连接
+   NioSctpServerChannel，异步的 Sctp 服务器端连接 这些通道涵盖了 UDP 和 TCP网络 IO以及文件 IO.

#### Selector

Netty基于Selector对象实现I/O多路复用，通过 Selector, 一个线程可以监听多个连接的Channel事件, 当向一个Selector中注册Channel 后，Selector 内部的机制就可以自动不断地查询(select) 这些注册的Channel是否有已就绪的I/O事件(例如可读, 可写, 网络连接完成等)，这样程序就可以很简单地使用一个线程高效地管理多个 Channel 。

#### NioEventLoop

NioEventLoop中维护了一个线程和任务队列，支持异步提交执行任务，线程启动时会调用NioEventLoop的run方法，执行I/O任务和非I/O任务：

+   I/O任务 即selectionKey中ready的事件，如accept、connect、read、write等，由processSelectedKeys方法触发。
+   非IO任务 添加到taskQueue中的任务，如register0、bind0等任务，由runAllTasks方法触发。

两种任务的执行时间比由变量ioRatio控制，默认为50，则表示允许非IO任务执行的时间与IO任务的执行时间相等。

#### NioEventLoopGroup

NioEventLoopGroup，主要管理eventLoop的生命周期，可以理解为一个线程池，内部维护了一组线程，每个线程(NioEventLoop)负责处理多个Channel上的事件，而一个Channel只对应于一个线程。

#### ChannelHandler

ChannelHandler是一个接口，处理I / O事件或拦截I / O操作，并将其转发到其ChannelPipeline(业务处理链)中的下一个处理程序。

ChannelHandler本身并没有提供很多方法，因为这个接口有许多的方法需要实现，方便使用期间，可以继承它的子类：

+   ChannelInboundHandler用于处理入站I / O事件
+   ChannelOutboundHandler用于处理出站I / O操作

或者使用以下适配器类：

+   ChannelInboundHandlerAdapter用于处理入站I / O事件
+   ChannelOutboundHandlerAdapter用于处理出站I / O操作
+   ChannelDuplexHandler用于处理入站和出站事件

#### ChannelHandlerContext

保存Channel相关的所有上下文信息，同时关联一个ChannelHandler对象

#### ChannelPipline

保存ChannelHandler的List，用于处理或拦截Channel的入站事件和出站操作。 ChannelPipeline实现了一种高级形式的拦截过滤器模式，使用户可以完全控制事件的处理方式，以及Channel中各个的ChannelHandler如何相互交互。

下图引用Netty的Javadoc4.1中ChannelPipline的说明，描述了ChannelPipeline中ChannelHandler通常如何处理I/O事件。 I/O事件由ChannelInboundHandler或ChannelOutboundHandler处理，并通过调用ChannelHandlerContext中定义的事件传播方法（例如ChannelHandlerContext.fireChannelRead（Object）和ChannelOutboundInvoker.write（Object））转发到其最近的处理程序。

```auto
                                                 I/O Request
                                            via Channel or
                                        ChannelHandlerContext
                                                      |
  +---------------------------------------------------+---------------+
  |                           ChannelPipeline         |               |
  |                                                  \|/              |
  |    +---------------------+            +-----------+----------+    |
  |    | Inbound Handler  N  |            | Outbound Handler  1  |    |
  |    +----------+----------+            +-----------+----------+    |
  |              /|\                                  |               |
  |               |                                  \|/              |
  |    +----------+----------+            +-----------+----------+    |
  |    | Inbound Handler N-1 |            | Outbound Handler  2  |    |
  |    +----------+----------+            +-----------+----------+    |
  |              /|\                                  .               |
  |               .                                   .               |
  | ChannelHandlerContext.fireIN_EVT() ChannelHandlerContext.OUT_EVT()|
  |        [ method call]                       [method call]         |
  |               .                                   .               |
  |               .                                  \|/              |
  |    +----------+----------+            +-----------+----------+    |
  |    | Inbound Handler  2  |            | Outbound Handler M-1 |    |
  |    +----------+----------+            +-----------+----------+    |
  |              /|\                                  |               |
  |               |                                  \|/              |
  |    +----------+----------+            +-----------+----------+    |
  |    | Inbound Handler  1  |            | Outbound Handler  M  |    |
  |    +----------+----------+            +-----------+----------+    |
  |              /|\                                  |               |
  +---------------+-----------------------------------+---------------+
                  |                                  \|/
  +---------------+-----------------------------------+---------------+
  |               |                                   |               |
  |       [ Socket.read() ]                    [ Socket.write() ]     |
  |                                                                   |
  |  Netty Internal I/O Threads (Transport Implementation)            |
  +-------------------------------------------------------------------+

123456789101112131415161718192021222324252627282930313233343536373839
```

入站事件由自下而上方向的入站处理程序处理，如图左侧所示。 入站Handler处理程序通常处理由图底部的I / O线程生成的入站数据。 通常通过实际输入操作（例如SocketChannel.read（ByteBuffer））从远程读取入站数据。

出站事件由上下方向处理，如图右侧所示。 出站Handler处理程序通常会生成或转换出站传输，例如write请求。 I/O线程通常执行实际的输出操作，例如SocketChannel.write（ByteBuffer）。

在 Netty 中每个 Channel 都有且仅有一个 ChannelPipeline 与之对应, 它们的组成关系如下:

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJkYzhjZDFhMmY?x-oss-process=image/format,png)

一个 Channel 包含了一个 ChannelPipeline, 而 ChannelPipeline 中又维护了一个由 ChannelHandlerContext 组成的双向链表, 并且每个 ChannelHandlerContext 中又关联着一个 ChannelHandler。入站事件和出站事件在一个双向链表中，入站事件会从链表head往后传递到最后一个入站的handler，出站事件会从链表tail往前传递到最前一个出站的handler，两种类型的handler互不干扰。

### 27、聊聊：Netty服务端过程初始化并启动过程

初始化并启动Netty服务端过程如下：

```java
    public static void main(String[] args) {
        // 创建mainReactor
        NioEventLoopGroup boosGroup = new NioEventLoopGroup();
        // 创建工作线程组
        NioEventLoopGroup workerGroup = new NioEventLoopGroup();

        final ServerBootstrap serverBootstrap = new ServerBootstrap();
        serverBootstrap 
                 // 组装NioEventLoopGroup 
                .group(boosGroup, workerGroup)
                 // 设置channel类型为NIO类型
                .channel(NioServerSocketChannel.class)
                // 设置连接配置参数
                .option(ChannelOption.SO_BACKLOG, 1024)
                .childOption(ChannelOption.SO_KEEPALIVE, true)
                .childOption(ChannelOption.TCP_NODELAY, true)
                // 配置入站、出站事件handler
                .childHandler(new ChannelInitializer<NioSocketChannel>() {
                    @Override
                    protected void initChannel(NioSocketChannel ch) {
                        // 配置入站、出站事件channel
                        ch.pipeline().addLast(...);
                        ch.pipeline().addLast(...);
                    }
    });

        // 绑定端口
        int port = 8080;
        serverBootstrap.bind(port).addListener(future -> {
            if (future.isSuccess()) {
                System.out.println(new Date() + ": 端口[" + port + "]绑定成功!");
            } else {
                System.err.println("端口[" + port + "]绑定失败!");
            }
        });
}


```

基本过程如下：

1 初始化创建2个NioEventLoopGroup，其中boosGroup用于Accetpt连接建立事件并分发请求， workerGroup用于处理I/O读写事件和业务逻辑

2 基于ServerBootstrap(服务端启动引导类)，配置EventLoopGroup、Channel类型，连接参数、配置入站、出站事件handler

3 绑定端口，开始工作

### 服务端Netty的工作架构图

结合上面的介绍的Netty Reactor模型，介绍服务端Netty的工作架构图：

![服务端Netty Reactor工作架构图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAxOC8xMS8xLzE2NmNjYmJkYzlhN2NhYmU?x-oss-process=image/format,png)

server端包含1个Boss NioEventLoopGroup和1个Worker NioEventLoopGroup，NioEventLoopGroup相当于1个事件循环组，这个组里包含多个事件循环NioEventLoop，每个NioEventLoop包含1个selector和1个事件循环线程。

每个Boss NioEventLoop循环执行的任务包含3步：

1 轮询accept事件

2 处理accept I/O事件，与Client建立连接，生成NioSocketChannel，并将NioSocketChannel注册到某个Worker NioEventLoop的Selector上 \*3 处理任务队列中的任务，runAllTasks。

任务队列中的任务包括用户调用eventloop.execute或schedule执行的任务，或者其它线程提交到该eventloop的任务。

每个Worker NioEventLoop循环执行的任务包含3步：

1 轮询read、write事件；

2 处I/O事件，即read、write事件，在NioSocketChannel可读、可写事件发生时进行处理

3 处理任务队列中的任务，runAllTasks。

### 任务队列的使用场景

其中任务队列中的task有3种典型使用场景

1 用户程序自定义的普通任务

```java
ctx.channel().eventLoop().execute(new Runnable() {
    @Override
    public void run() {
        //...
    }
});


```

2 非当前reactor线程调用channel的各种方法

例如在推送系统的业务线程里面，根据用户的标识，找到对应的channel引用，然后调用write类方法向该用户推送消息，就会进入到这种场景。最终的write会提交到任务队列中后被异步消费。

3 用户自定义定时任务

```java
ctx.channel().eventLoop().schedule(new Runnable() {
    @Override
    public void run() {

    }
}, 60, TimeUnit.SECONDS);


```

### 28、聊一下：Netty ByteBuf的特点？

这里想要比较两种Buffer,对比ByteBuffer得出ByteBuf的优点点,

我们首先要做的就是总结ByteBuf的特点以及相比ByteBuffer,这个特点如何成为优点：  
**一：ByteBuf读写指针**  
在ByteBuffer中,读写指针都是position,

而在ByteBuf中,读写指针分别为readerIndex和writerIndex,

直观看上去ByteBuffer仅用了一个指针就实现了两个指针的功能,节省了变量,但是当对于ByteBuffer的读写状态切换的时候必须要调用flip方法,而当下一次写之前,必须要将Buffe中的内容读完,再调用clear方法。

每次读之前调用flip,写之前调用clear,这样无疑给开发带来了繁琐的步骤,而且内容没有读完是不能写的,这样非常不灵活。

相比之下我们看看ByteBuf,读的时候仅仅依赖readerIndex指针,写的时候仅仅依赖writerIndex指针,不需每次读写之前调用对应的方法,而且没有必须一次读完的限制。  
**二：ByteBuf引用计数**  
ByteBuf扩展了ReferenceCountered接口,这个接口定义的功能主要是引用计数：  
ReferenceCountered接口定义  
也就是所有对ByteBuf的实现,都要实现引用计数,Netty对Buffer资源进行了显式的管理,这部分要结合Netty的内存池技术理解,当Buffer引用+1的时候,需要调用retain来让refCnt+1,当Buffer引用数-1的时候需要调用release来让refCnt-1,当refCnt变为0的时候Netty为pooled和unpooled的不同buffer提供了不同的实现,通常对于非内存池的用法,Netty把Buffer的内存回收交给了垃圾回收器,对于内存池的用法,Netty对内存的回收实际上是回收到内存池内,以提供下一次的申请所使用,关于内存池这部分可以参考我之前的一篇文章。  
**三：池化Buffer资源**  
由于Netty是一个NIO网络框架,因此对于Buffer的使用如果基于直接内存DirectBuffer：实现的话,将会大大提高I/O操作的效率,然而DirectBuffer和HeapBuffer相比之下除了I/O操作效率高之外还有一个天生的缺点,即对于DirectBuffer的申请相比HeapBuffer效率更低,因此Netty结合引用计数实现了PolledBuffer,即池化的用法,当引用计数等于0的时候,Netty将Buffer回收致池中,在下一次申请Buffer的没某个时刻会被复用。Netty这样做的基本想法是我们花了很大的力气申请了一块内存,不能轻易让他被回收呀,能重复利用当然重复利用咯。  
**四：ByteBuffer才能和Channel打交道**  
归根结底,站在NIO的立场上所有的缓冲区要想和Channel打交道,换句话说也就是从网络Channel读取数据的时候,都是从Channel到ByteBuffer,从缓冲区写的网上上的时候,都是从ByteBuffer到Channel。因此,当Netty监听到I/O读事件的时候,会将自己流从Channel读到ByteBuffer而不是ByteBuf,see below:  
return in.read((ByteBuffer) internalNioBuffer().clear().position(index).limit(index + length));  
上面是ByteBuf的其中一个具体的读实现,可以看出ByteBuf维护着一个内部的ByteBuffer,叫做internalNioBuffer。当需要将字节流写入网络的时候,

需要将ByteBuf转换为ByteBuffer:

```auto
   ByteBuffer tmpBuf;
     if (internal) {
       tmpBuf = internalNioBuffer();
     } else {
       tmpBuf = ByteBuffer.wrap(array);
     }
     return out.write((ByteBuffer) tmpBuf.clear().position(index).limit(index + length));
   }


```

### 29、简单聊聊：Netty的线程模型的三种使用方式？

**单线程模型** ：

一个线程需要执行处理所有的 accept、read、decode、process、encode、send 事件。对于高负载、高并发，并且对性能要求比较高的场景不适用。

对应到 Netty 代码是下面这样的

使用 NioEventLoopGroup 类的无参构造函数设置线程数量的默认值就是 \*\*CPU 核心数 *2* 。

```auto
  //1.eventGroup既用于处理客户端连接，又负责具体的处理。
  EventLoopGroup eventGroup = new NioEventLoopGroup(1);
  //2.创建服务端启动引导/辅助类：ServerBootstrap
  ServerBootstrap b = new ServerBootstrap();
            boobtstrap.group(eventGroup, eventGroup)
            //......
```

**多线程模型**

一个 Acceptor 线程只负责监听客户端的连接，一个 NIO 线程池负责具体处理：accept、read、decode、process、encode、send 事件。满足绝大部分应用场景，并发连接量不大的时候没啥问题，但是遇到并发连接大的时候就可能会出现问题，成为性能瓶颈。

对应到 Netty 代码是下面这样的：

```auto
// 1.bossGroup 用于接收连接，workerGroup 用于具体的处理
EventLoopGroup bossGroup = new NioEventLoopGroup(1);
EventLoopGroup workerGroup = new NioEventLoopGroup();
try {
  //2.创建服务端启动引导/辅助类：ServerBootstrap
  ServerBootstrap b = new ServerBootstrap();
  //3.给引导类配置两大线程组,确定了线程模型
  b.group(bossGroup, workerGroup)
    //......
```

![img](https://img-blog.csdnimg.cn/img_convert/d38064324b01b44728d65301237af685.png#alt=)

**主从多线程模型**

从一个 主线程 NIO 线程池中选择一个线程作为 Acceptor 线程，绑定监听端口，接收客户端连接的连接，其他线程负责后续的接入认证等工作。连接建立完成后，Sub NIO 线程池负责具体处理 I/O 读写。如果多线程模型无法满足你的需求的时候，可以考虑使用主从多线程模型 。

```auto
// 1.bossGroup 用于接收连接，workerGroup 用于具体的处理
EventLoopGroup bossGroup = new NioEventLoopGroup();
EventLoopGroup workerGroup = new NioEventLoopGroup();
try {
  //2.创建服务端启动引导/辅助类：ServerBootstrap
  ServerBootstrap b = new ServerBootstrap();
  //3.给引导类配置两大线程组,确定了线程模型
  b.group(bossGroup, workerGroup)
    //......
```

![img](https://img-blog.csdnimg.cn/img_convert/87497884c7342ffb9909a8a04b577a66.png#alt=)

### 30、默认情况 Netty 起多少线程？何时启动？

Netty 默认是 CPU 处理器数的两倍，bind 完之后启动。

### 31、TCP 粘包/拆包的原因及解决方法？

#### TCP粘包/分包的原因：

TCP是以流的方式来处理数据，一个完整的包可能会被TCP拆分成多个包进行发送，也可能把小的封装成一个大的数据包发送。

深层次的原因，是TCP/IP协议，是四层协议，会逐层进行数据的封装和分用。

而每一层都有自己的特定标识和头部，每一层的数据

数据通过互联网传输的时候不可能是光秃秃的不加标识，如果这样数据就会乱。所以数据在发送的时候，需要加上特定标识，加上特定标识的过程叫做数据的封装，在数据使用的时候再去掉特定标识，去掉特定标识的过程就叫做分用。

TCP/IP协议的数据封装和分用过程，大致如下图所示：  
[![在这里插入图片描述](https://img-blog.csdnimg.cn/20210308122819964.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NyYXp5bWFrZXJjaXJjbGU=,size_16,color_FFFFFF,t_70#pic_center)](https://img-blog.csdnimg.cn/20210308122819964.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NyYXp5bWFrZXJjaXJjbGU=,size_16,color_FFFFFF,t_70#pic_center)

图：TCP/IP协议的数据封装和分用过程TCP/IP协议是层层



在TCP/IP分层中，OSI的应用层、表示层、会话层全都统一为应用层，而底层的物理层和链路层又统一为接口层。每个TCP/IP分层都对应一些协议，这些协议组成了TCP/IP协议栈。

最顶层的是应用层协议，比如HTTP协议、DNS协议、FTP协议、POP3协议等。

传输层包含两个协议，TCP协议和UDP协议，在这一层将指定通信端口。

网络层包括ARP协议、IP协议、ICMP协议、IGMP协议等等，网络层的协议有些并不完全属于网络层，有可能向下跨到链路层，但总的来说，将它们都归类到网络层协议。

注意，上图中只有链路层部分才是以太网帧的数据，所以7字节的前同步码（Preamble）、1字节的帧起始定界符、12字节的帧间距不属于以太网帧，它们属于物理层。其中，帧间距的存在，说明每个帧之间是间隔传输的，并不是完全连续传输。

主要看以太网帧格式。首先是6字节的目标MAC地址和6字节的源MAC地址，然后是可选的tag标记，一般当它不存在，之后是表示类型的2个字节，接着便是数据包部分，尾部是一个4字节的CRC的帧校验码。

目标MAC字段记录了目标的MAC地址，当某网卡或适配器接收到了一个以太网帧，如果它的MAC地址正好是帧中记录的目标地址，则将该帧解封后的数据包传递给网络层。此外，如果收到的是广播帧（目标MAC地址为FF-FF-FF-FF-FF-FF），则也将其传递给网络层，但如果收到目标MAC地址不是本接口地址的任何数据帧，都将直接丢弃。

源MAC地址字段记录的是该帧的出口MAC地址。

由于信道是所有主机共享的，如果数据帧太长就会出现有的主机长时间不能发送数据，而且有的发送数据可能超出接收端的缓冲区大小，造成缓冲溢出。为避免单一主机占用信道时间过长，规定了以太网帧的最大帧长为1500。

由于信道是所有主机共享的，如果数据帧太长就会出现有的主机长时间不能发送数据，而且有的发送数据可能超出接收端的缓冲区大小，造成缓冲溢出。为避免单一主机占用信道时间过长，规定了以太网帧的最大帧长为1500。

#### MTU

在网络中，最大传输单元（MTU）指通过联网设备可以接收的最大数据包的值。

MTU可以 想象为高速公路地下通道或隧道的高度限制：超过高度限制的汽车和卡车无法通过，就像超过网络 MTU 的数据包无法通过该网络一样。

不过，与汽车和卡车不同的是，超过 MTU 的数据包可被分解成较小的碎片，从而能通过网络。

这个过程称为分片。分片的数据包在到达目的地后便会重新组装。

MTU 以字节数为单位，一个“字节”等于 8 位信息，即 8 个一和零。1,500 字节是最大 MTU 大小。

#### MSS

MSS: Maximum Segment Size 最大报文段长度

MSS是最大报文段长度的缩写，是TCP协议里面的一个概念。

MSS是TCP\[数据包\]每次能够传输的最大数据分段。

为了达到最佳的传输效能，TCP协议在建立连接的时候通常要协商双方的MSS值，

这个值TCP协议在实现的时候往往用MTU值代替（需要减去IP数据包包头的大小20Bytes和TCP数据段的包头20Bytes）所以一般MSS值1460

通讯双方会根据双方提供的MSS值得最小值确定为这次连接的最大MSS值。

> 注：最大报文段长度MSS这个名词*很容易引起误解*。
>
> MSS是TCP报文段中的数据字段的最大长度。数据字段加上TCP首部才等于整个的TCP报文段。所以MSS并不是TCP报文段的最大长度，而是：

MSS=TCP报文段长度-TCP首部长度-IP首部。

MSS（Maximum Segment Size，最大报文长度），是TCP协议定义的一个选项，MSS选项用于在TCP连接建立时，收发双方协商通信时每一个报文段所能承载的最大数据长度。

#### 应用层的半包问题（拆包和粘包）

拆包：一个完整的应用包可能会被 TCP 拆分成多个包进行发送。

粘包：也可能把小应用包的封装成一个大的 TCP数据包发送。

应用程序写入的字节大小大于套接字发送缓冲区的大小，会发生拆包现象，

而应用程序写入数据小于套接字缓冲区大小，网卡将应用多次写入的数据发送到网络上，这将会发生粘包现象。

```auto
实际上，拆包、粘包的本质，就是受限于各层协议净菏的大小不一，

都要对上层的数据进行重新组装，

上层的协议收到下层的数据包，都有可能出现拆包、粘包问题。

```

当TCP帧的payload（净荷）TCP报文长度-TCP头部长度>MSS (1460)的时候， 将发生拆包，进行MSS大小的TCP分段，

以太网帧的payload（净荷）大于MTU（1500字节）进行太网帧 分片。

#### 拆包和粘包解决方法

#### 解决方法

Netty中提供了多个 Decoder 解析类 用于解决上述问题：

+   FixedLengthFrameDecoder 、LengthFieldBasedFrameDecoder ，固定长度是消息头指定消息长度的一种形式，进行粘包拆包处理的。

+   LineBasedFrameDecoder 、DelimiterBasedFrameDecoder ，换行是于指定消息边界方式的一种形式，进行消息粘


### 32、Netty 中有哪种重要组件？

+   Channel：Netty 网络操作抽象类，它除了包括基本的 I/O 操作，如 bind、connect、read、write 等。
+   EventLoop：主要是配合 Channel 处理 I/O 操作，用来处理连接的生命周期中所发生的事情。
+   ChannelFuture：Netty 框架中所有的 I/O 操作都为异步的，因此我们需要 ChannelFuture 的 addListener()注册一个 ChannelFutureListener 监听事件，当操作执行成功或者失败时，监听就会自动触发返回结果。
+   ChannelHandler：充当了所有处理入站和出站数据的逻辑容器。ChannelHandler 主要用来处理各种事件，这里的事件很广泛，比如可以是连接、数据接收、异常、数据转换等。
+   ChannelPipeline：为 ChannelHandler 链提供了容器，当 channel 创建时，就会被自动分配到它专属的 ChannelPipeline，这个关联是永久性的。

### 33、Netty 发送消息有几种方式？

Netty 有两种发送消息的方式：

+   直接写入 Channel 中，消息从 ChannelPipeline 当中尾部开始移动；
+   写入和 ChannelHandler 绑定的 ChannelHandlerContext 中，消息从 ChannelPipeline 中的下一个 ChannelHandler 中移动。

### 34、什么是 Netty 的零拷贝？

Netty 的零拷贝主要包含三个方面：

+   Netty 的接收和发送 ByteBuffer 采用 DIRECT BUFFERS，使用堆外直接内存进行 Socket 读写，不需要进行字节缓冲区的二次拷贝。如果使用传统的堆内存（HEAP BUFFERS）进行 Socket 读写，JVM 会将堆内存 Buffer 拷贝一份到直接内存中，然后才写入 Socket 中。相比于堆外直接内存，消息在发送过程中多了一次缓冲区的内存拷贝。
+   Netty 提供了组合 Buffer 对象，可以聚合多个 ByteBuffer 对象，用户可以像操作一个 Buffer 那样方便的对组合 Buffer 进行操作，避免了传统通过内存拷贝的方式将几个小 Buffer 合并成一个大的 Buffer。
+   Netty 的文件传输采用了 transferTo 方法，它可以直接将文件缓冲区的数据发送到目标 Channel，避免了传统通过循环 write 方式导致的内存拷贝问题。

这个答案不完整，具体请参考 视频

### 35、了解哪几种序列化协议？

序列化（编码）是将对象序列化为二进制形式（字节数组），主要用于网络传输、数据持久化等；而反序列化（解码）则是将从网络、磁盘等读取的字节数组还原成原始对象，主要用于网络传输对象的解码，以便完成远程调用。

影响序列化性能的关键因素：序列化后的码流大小（网络带宽的占用）、序列化的性能（CPU资源占用）；是否支持跨语言（异构系统的对接和开发语言切换）。

Java默认提供的序列化：无法跨语言、序列化后的码流太大、序列化的性能差

XML，优点：人机可读性好，可指定元素或特性的名称。缺点：序列化数据只包含数据本身以及类的结构，不包括类型标识和程序集信息；只能序列化公共属性和字段；不能序列化方法；文件庞大，文件格式复杂，传输占带宽。适用场景：当做配置文件存储数据，实时数据转换。

JSON，是一种轻量级的数据交换格式，优点：兼容性高、数据格式比较简单，易于读写、序列化后数据较小，可扩展性好，兼容性好、与XML相比，其协议比较简单，解析速度比较快。缺点：数据的描述性比XML差、不适合性能要求为ms级别的情况、额外空间开销比较大。适用场景（可替代ＸＭＬ）：跨防火墙访问、可调式性要求高、基于Web browser的Ajax请求、传输数据量相对小，实时性要求相对低（例如秒级别）的服务。

Fastjson，采用一种“假定有序快速匹配”的算法。优点：接口简单易用、目前java语言中最快的json库。缺点：过于注重快，而偏离了“标准”及功能性、代码质量不高，文档不全。适用场景：协议交互、Web输出、Android客户端

Thrift，不仅是序列化协议，还是一个RPC框架。优点：序列化后的体积小, 速度快、支持多种语言和丰富的数据类型、对于数据字段的增删具有较强的兼容性、支持二进制压缩编码。缺点：使用者较少、跨防火墙访问时，不安全、不具有可读性，调试代码时相对困难、不能与其他传输层协议共同使用（例如HTTP）、无法支持向持久层直接读写数据，即不适合做数据持久化序列化协议。适用场景：分布式系统的RPC解决方案

Avro，Hadoop的一个子项目，解决了JSON的冗长和没有IDL的问题。优点：支持丰富的数据类型、简单的动态语言结合功能、具有自我描述属性、提高了数据解析速度、快速可压缩的二进制数据形式、可以实现远程过程调用RPC、支持跨编程语言实现。缺点：对于习惯于静态类型语言的用户不直观。适用场景：在Hadoop中做Hive、Pig和MapReduce的持久化数据格式。

Protobuf，将数据结构以.proto文件进行描述，通过代码生成工具可以生成对应数据结构的POJO对象和Protobuf相关的方法和属性。优点：序列化后码流小，性能高、结构化数据存储格式（XML JSON等）、通过标识字段的顺序，可以实现协议的前向兼容、结构化的文档更容易管理和维护。缺点：需要依赖于工具生成代码、支持的语言相对较少，官方只支持Java 、C++ 、python。适用场景：对性能要求高的RPC调用、具有良好的跨防火墙的访问属性、适合应用层对象的持久化

其它

protostuff 基于protobuf协议，但不需要配置proto文件，直接导包即可  
Jboss marshaling 可以直接序列化java类， 无须实java.io.Serializable接口  
Message pack 一个高效的二进制序列化格式  
Hessian 采用二进制协议的轻量级remoting onhttp工具  
kryo 基于protobuf协议，只支持java语言,需要注册（Registration），然后序列化（Output），反序列化（Input）

### 36、如何选择序列化协议？

具体场景

对于公司间的系统调用，如果性能要求在100ms以上的服务，基于XML的SOAP协议是一个值得考虑的方案。  
基于Web browser的Ajax，以及Mobile app与服务端之间的通讯，JSON协议是首选。对于性能要求不太高，或者以动态类型语言为主，或者传输数据载荷很小的的运用场景，JSON也是非常不错的选择。  
对于调试环境比较恶劣的场景，采用JSON或XML能够极大的提高调试效率，降低系统开发成本。  
当对性能和简洁性有极高要求的场景，Protobuf，Thrift，Avro之间具有一定的竞争关系。  
对于T级别的数据的持久化应用场景，Protobuf和Avro是首要选择。如果持久化后的数据存储在hadoop子项目里，Avro会是更好的选择。

对于持久层非Hadoop项目，以静态类型语言为主的应用场景，Protobuf会更符合静态类型语言工程师的开发习惯。由于Avro的设计理念偏向于动态类型语言，对于动态语言为主的应用场景，Avro是更好的选择。  
如果需要提供一个完整的RPC解决方案，Thrift是一个好的选择。  
如果序列化之后需要支持不同的传输层协议，或者需要跨防火墙访问的高性能场景，Protobuf可以优先考虑。  
protobuf的数据类型有多种：bool、double、float、int32、int64、string、bytes、enum、message。protobuf的限定符：required: 必须赋值，不能为空、optional:字段可以赋值，也可以不赋值、repeated: 该字段可以重复任意次数（包括0次）、枚举；只能用指定的常量集中的一个值作为其值；

protobuf的基本规则：每个消息中必须至少留有一个required类型的字段、包含0个或多个optional类型的字段；repeated表示的字段可以包含0个或多个数据；\[1,15\]之内的标识号在编码的时候会占用一个字节（常用），\[16,2047\]之内的标识号则占用2个字节，标识号一定不能重复、使用消息类型，也可以将消息嵌套任意多层，可用嵌套消息类型来代替组。

protobuf的消息升级原则：不要更改任何已有的字段的数值标识；不能移除已经存在的required字段，optional和repeated类型的字段可以被移除，但要保留标号不能被重用。新添加的字段必须是optional或repeated。因为旧版本程序无法读取或写入新增的required限定符的字段。

编译器为每一个消息类型生成了一个.java文件，以及一个特殊的Builder类（该类是用来创建消息类接口的）。如：UserProto.User.Builder builder = UserProto.User.newBuilder();builder.build()；

Netty中的使用：ProtobufVarint32FrameDecoder 是用于处理半包消息的解码类；ProtobufDecoder(UserProto.User.getDefaultInstance())这是创建的UserProto.java文件中的解码类；ProtobufVarint32LengthFieldPrepender 对protobuf协议的消息头上加上一个长度为32的整形字段，用于标志这个消息的长度的类；ProtobufEncoder 是编码类

将StringBuilder转换为ByteBuf类型：copiedBuffer()方法

### 37、Netty 支持哪些心跳类型设置？

+   readerIdleTime：为读超时时间（即测试端一定时间内未接受到被测试端消息）。
+   writerIdleTime：为写超时时间（即测试端一定时间内向被测试端发送消息）。
+   allIdleTime：所有类型的超时时间。

### 38、为什么没有使用Netty5 ？

现在稳定推荐使用的主流版本还是Netty4，

Netty5 中使用了 ForkJoinPool，增加了代码的复杂度，但是对性能的改善却不明显，

所以Netty5 版本不推荐使用，官网也没有提供下载链接。

Netty 入门门槛相对较高，其实是因为这方面的资料较少，并不是因为他有多难，大家其实都可以像搞透 Spring 一样搞透 Netty。

在学习之前，建议先理解透整个框架原理结构，运行过程，可以少走很多弯路。

### 38、简单说说：NIOEventLoopGroup源码？

NioEventLoopGroup(其实是MultithreadEventExecutorGroup) 内部维护一个类型为 EventExecutor children \[\],

默认大小是处理器核数 \* 2, 这样就构成了一个线程池，初始化EventExecutor时NioEventLoopGroup重载newChild方法，所以children元素的实际类型为NioEventLoop。

线程启动时调用SingleThreadEventExecutor的构造方法，执行NioEventLoop类的run方法，首先会调用hasTasks()方法判断当前taskQueue是否有元素。

如果taskQueue中有元素，执行 selectNow() 方法，最终执行selector.selectNow()，该方法会立即返回。如果taskQueue没有元素，执行 select(oldWakenUp) 方法

select ( oldWakenUp) 方法解决了 Nio 中的 bug，具体的方案为：

selectCnt 用来记录selector.select方法的执行次数和标识是否执行过selector.selectNow()，若触发了epoll的空轮询bug，则会反复执行selector.select(timeoutMillis)，变量selectCnt 会逐渐变大，当selectCnt 达到阈值（默认512），则执行rebuildSelector方法，进行selector重建，解决cpu占用100%的bug。

rebuildSelector方法先通过openSelector方法创建一个新的selector。然后将old selector的selectionKey执行cancel。最后将old selector的channel重新注册到新的selector中。rebuild后，需要重新执行方法selectNow，检查是否有已ready的selectionKey。

接下来调用processSelectedKeys 方法（处理I/O任务），当selectedKeys != null时，调用processSelectedKeysOptimized方法，迭代 selectedKeys 获取就绪的 IO 事件的selectkey存放在数组selectedKeys中, 然后为每个事件都调用 processSelectedKey 来处理它，processSelectedKey 中分别处理OP\_READ；OP\_WRITE；OP\_CONNECT事件。

最后调用runAllTasks方法（非IO任务），该方法首先会调用fetchFromScheduledTaskQueue方法，把scheduledTaskQueue中已经超过延迟执行时间的任务移到taskQueue中等待被执行，然后依次从taskQueue中取任务执行，每执行64个任务，进行耗时检查，如果已执行时间超过预先设定的执行时间，则停止执行非IO任务，避免非IO任务太多，影响IO任务的执行。

每个NioEventLoop对应一个线程和一个Selector，NioServerSocketChannel会主动注册到某一个NioEventLoop的Selector上，NioEventLoop负责事件轮询。

Outbound 事件都是请求事件, 发起者是 Channel，处理者是 unsafe，通过 Outbound 事件进行通知，传播方向是 tail到head。Inbound 事件发起者是 unsafe，事件的处理者是 Channel, 是通知事件，传播方向是从头到尾。

内存管理机制，首先会预申请一大块内存Arena，Arena由许多Chunk组成，而每个Chunk默认由2048个page组成。Chunk通过AVL树的形式组织Page，每个叶子节点表示一个Page，而中间节点表示内存区域，节点自己记录它在整个Arena中的偏移地址。当区域被分配出去后，中间节点上的标记位会被标记，这样就表示这个中间节点以下的所有节点都已被分配了。大于8k的内存分配在poolChunkList中，而PoolSubpage用于分配小于8k的内存，它会把一个page分割成多段，进行内存分配。

ByteBuf的特点：支持自动扩容（4M），保证put方法不会抛出异常、通过内置的复合缓冲类型，实现零拷贝（zero-copy）；不需要调用flip()来切换读/写模式，读取和写入索引分开；方法链；引用计数基于AtomicIntegerFieldUpdater用于内存回收；PooledByteBuf采用二叉树来实现一个内存池，集中管理内存的分配和释放，不用每次使用都新建一个缓冲区对象。UnpooledHeapByteBuf每次都会新建一个缓冲区对象。

### 

### 39、问题：JDK NIO中Epoll空轮询Bug产生的原因以及Netty中是如何解决的

#### 产生原因

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201226165322589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwNzUxNTUy,size_16,color_FFFFFF,t_70)  
正常情况下，selector.select()操作是阻塞的，只有被监听的fd有读写操作时，才被唤醒。

但是，在这个bug中，没有任何fd有读写请求，但是select()操作依旧被唤醒很显然，这种情况下，selectedKeys()返回的是个空数组，然后按照逻辑执行到while(true)处，循环执行，导致死循环。

#### Netty的解决方法

1.  对Selector的select操作周期进行统计，每完成一次空的select操作进行一次计数。
2.  若在某个周期内连续发生N次空轮询，则触发了epoll死循环bug。
3.  重建Selector，判断是否是其他线程发起的重建请求，若不是则将原SocketChannel从旧的Selector上去除注册，重新注册到新的Selector上，并将原来的Selector关闭。

#### **暗语**：

以上的问题和答案，来自于网络（一搜一大把），并且点击率非常高。

以上问题，出现了知识性错误，不是答案有误，而是问题有误。

因为： 是select空轮训导致cpu100% 的问题，二epoll并没有出现空轮训导致cpu100% 的问题

所以， 使用epoll 反应器就可以了

### 40、简单说说：Netty如何解决Selector空轮询BUG的策略

[Netty解决Selector空轮询BUG的策略（图解+秒懂+史上最全）](https://www.cnblogs.com/crazymakercircle/p/15370299.html)

### 41、Netty如何实现断线重连?

在实现TCP长连接功能中，客户端断线重连是一个很常见的问题，当我们使用netty实现断线重连时，是否考虑过如下几个问题：

+   如何监听到客户端和服务端连接断开 ?
+   如何实现断线后重新连接 ?
+   netty客户端线程给多大比较合理 ?

**实现思路**

客户端在监测到与服务器端的连接断开后，或者一开始就无法连接的情况下，使用指定的重连策略进行重连操作，直到重新建立连接或重试次数耗尽。

对于如何监测连接是否断开，则是通过重写ChannelInboundHandler#channelInactive来实现，但连接不可用，该方法会被触发，所以只需要在该方法做好重连工作即可。

**代码实现**

> 注：以下代码都是在上面心跳机制的基础上修改/添加的。

因为断线重连是客户端的工作，所以只需对客户端代码进行修改。

**重试策略**

**RetryPolicy —— 重试策略接口**

```applescript
public interface RetryPolicy {

    /**
     * Called when an operation has failed for some reason. This method should return
     * true to make another attempt.
     *
     * @param retryCount the number of times retried so far (0 the first time)
     * @return true/false
     */
    boolean allowRetry(int retryCount);

    /**
     * get sleep time in ms of current retry count.
     *
     * @param retryCount current retry count
     * @return the time to sleep
     */
    long getSleepTimeMs(int retryCount);
}
```

**ExponentialBackOffRetry —— 重连策略的默认实现**

```java
/**
 * <p>Retry policy that retries a set number of times with increasing sleep time between retries</p>
 */
public class ExponentialBackOffRetry implements RetryPolicy {

    private static final int MAX_RETRIES_LIMIT = 29;
    private static final int DEFAULT_MAX_SLEEP_MS = Integer.MAX_VALUE;

    private final Random random = new Random();
    private final long baseSleepTimeMs;
    private final int maxRetries;
    private final int maxSleepMs;

    public ExponentialBackOffRetry(int baseSleepTimeMs, int maxRetries) {
        this(baseSleepTimeMs, maxRetries, DEFAULT_MAX_SLEEP_MS);
    }

    public ExponentialBackOffRetry(int baseSleepTimeMs, int maxRetries, int maxSleepMs) {
        this.maxRetries = maxRetries;
        this.baseSleepTimeMs = baseSleepTimeMs;
        this.maxSleepMs = maxSleepMs;
    }

    @Override
    public boolean allowRetry(int retryCount) {
        if (retryCount < maxRetries) {
            return true;
        }
        return false;
    }

    @Override
    public long getSleepTimeMs(int retryCount) {
        if (retryCount < 0) {
            throw new IllegalArgumentException("retries count must greater than 0.");
        }
        if (retryCount > MAX_RETRIES_LIMIT) {
            System.out.println(String.format("maxRetries too large (%d). Pinning to %d", maxRetries, MAX_RETRIES_LIMIT));
            retryCount = MAX_RETRIES_LIMIT;
        }
        long sleepMs = baseSleepTimeMs * Math.max(1, random.nextInt(1 << retryCount));
        if (sleepMs > maxSleepMs) {
            System.out.println(String.format("Sleep extension too large (%d). Pinning to %d", sleepMs, maxSleepMs));
            sleepMs = maxSleepMs;
        }
        return sleepMs;
    }
}
```

**ReconnectHandler—— 重连处理器**

```java
@ChannelHandler.Sharable
public class ReconnectHandler extends ChannelInboundHandlerAdapter {

    private int retries = 0;
    private RetryPolicy retryPolicy;

    private TcpClient tcpClient;

    public ReconnectHandler(TcpClient tcpClient) {
        this.tcpClient = tcpClient;
    }

    @Override
    public void channelActive(ChannelHandlerContext ctx) throws Exception {
        System.out.println("Successfully established a connection to the server.");
        retries = 0;
        ctx.fireChannelActive();
    }

    @Override
    public void channelInactive(ChannelHandlerContext ctx) throws Exception {
        if (retries == 0) {
            System.err.println("Lost the TCP connection with the server.");
            ctx.close();
        }

        boolean allowRetry = getRetryPolicy().allowRetry(retries);
        if (allowRetry) {

            long sleepTimeMs = getRetryPolicy().getSleepTimeMs(retries);

            System.out.println(String.format("Try to reconnect to the server after %dms. Retry count: %d.", sleepTimeMs, ++retries));

            final EventLoop eventLoop = ctx.channel().eventLoop();
            eventLoop.schedule(() -> {
                System.out.println("Reconnecting ...");
                tcpClient.connect();
            }, sleepTimeMs, TimeUnit.MILLISECONDS);
        }
        ctx.fireChannelInactive();
    }

    private RetryPolicy getRetryPolicy() {
        if (this.retryPolicy == null) {
            this.retryPolicy = tcpClient.getRetryPolicy();
        }
        return this.retryPolicy;
    }
}
```

**ClientHandlersInitializer**

在之前的基础上，添加了重连处理器ReconnectHandler。

```reasonml
public class ClientHandlersInitializer extends ChannelInitializer<SocketChannel> {

    private ReconnectHandler reconnectHandler;
    private EchoHandler echoHandler;

    public ClientHandlersInitializer(TcpClient tcpClient) {
        Assert.notNull(tcpClient, "TcpClient can not be null.");
        this.reconnectHandler = new ReconnectHandler(tcpClient);
        this.echoHandler = new EchoHandler();
    }

    @Override
    protected void initChannel(SocketChannel ch) throws Exception {
        ChannelPipeline pipeline = ch.pipeline();
        pipeline.addLast(this.reconnectHandler);
        pipeline.addLast(new LengthFieldBasedFrameDecoder(Integer.MAX_VALUE, 0, 4, 0, 4));
        pipeline.addLast(new LengthFieldPrepender(4));
        pipeline.addLast(new StringDecoder(CharsetUtil.UTF_8));
        pipeline.addLast(new StringEncoder(CharsetUtil.UTF_8));
        pipeline.addLast(new Pinger());
    }
}
```

**TcpClient**

在之前的基础上添加重连、重连策略的支持。

```arduino
public class TcpClient {

    private String host;
    private int port;
    private Bootstrap bootstrap;
    /** 重连策略 */
    private RetryPolicy retryPolicy;
    /** 将<code>Channel</code>保存起来, 可用于在其他非handler的地方发送数据 */
    private Channel channel;

    public TcpClient(String host, int port) {
        this(host, port, new ExponentialBackOffRetry(1000, Integer.MAX_VALUE, 60 * 1000));
    }

    public TcpClient(String host, int port, RetryPolicy retryPolicy) {
        this.host = host;
        this.port = port;
        this.retryPolicy = retryPolicy;
        init();
    }

    /**
     * 向远程TCP服务器请求连接
     */
    public void connect() {
        synchronized (bootstrap) {
            ChannelFuture future = bootstrap.connect(host, port);
            future.addListener(getConnectionListener());
            this.channel = future.channel();
        }
    }

    public RetryPolicy getRetryPolicy() {
        return retryPolicy;
    }

    private void init() {
        EventLoopGroup group = new NioEventLoopGroup();
        // bootstrap 可重用, 只需在TcpClient实例化的时候初始化即可.
        bootstrap = new Bootstrap();
        bootstrap.group(group)
                .channel(NioSocketChannel.class)
                .handler(new ClientHandlersInitializer(TcpClient.this));
    }

    private ChannelFutureListener getConnectionListener() {
        return new ChannelFutureListener() {
            @Override
            public void operationComplete(ChannelFuture future) throws Exception {
                if (!future.isSuccess()) {
                    future.channel().pipeline().fireChannelInactive();
                }
            }
        };
    }

    public static void main(String[] args) {
        TcpClient tcpClient = new TcpClient("localhost", 2222);
        tcpClient.connect();
    }

}
```

在测试之前，为了避开 Connection reset by peer 异常，可以稍微修改Pinger的ping()方法，添加if (second == 5)的条件判断。如下：

```reasonml
private void ping(Channel channel) {
        int second = Math.max(1, random.nextInt(baseRandom));
        if (second == 5) {
            second = 6;
        }
        System.out.println("next heart beat will send after " + second + "s.");
        ScheduledFuture<?> future = channel.eventLoop().schedule(new Runnable() {
            @Override
            public void run() {
                if (channel.isActive()) {
                    System.out.println("sending heart beat to the server...");
                    channel.writeAndFlush(ClientIdleStateTrigger.HEART_BEAT);
                } else {
                    System.err.println("The connection had broken, cancel the task that will send a heart beat.");
                    channel.closeFuture();
                    throw new RuntimeException();
                }
            }
        }, second, TimeUnit.SECONDS);

        future.addListener(new GenericFutureListener() {
            @Override
            public void operationComplete(Future future) throws Exception {
                if (future.isSuccess()) {
                    ping(channel);
                }
            }
        });
    }
```

**启动客户端**

先只启动客户端，观察控制台输出，可以看到类似如下日志：

![img](https://img-blog.csdnimg.cn/img_convert/98a949dbb696f71164a890285ad0d390.png)

断线重连测试——客户端控制台输出

可以看到，当客户端发现无法连接到服务器端，所以一直尝试重连。随着重试次数增加，重试时间间隔越大，但又不想无限增大下去，所以需要定一个阈值，比如60s。如上图所示，当下一次重试时间超过60s时，会打印Sleep extension too large(\*). Pinning to 60000，单位为ms。出现这句话的意思是，计算出来的时间超过阈值（60s），所以把真正睡眠的时间重置为阈值（60s）。

### 42、聊聊：Netty 如何实现心跳机制?

**何为心跳**

所谓心跳, 即在 TCP 长连接中, 客户端和服务器之间定期发送的一种特殊的数据包, 通知对方自己还在线, 以确保 TCP 连接的有效性.

> 注：心跳包还有另一个作用，经常被忽略，即：**一个连接如果长时间不用，防火墙或者路由器就会断开该连接。**

**如何实现**

**核心Handler —— IdleStateHandler**

在 Netty 中, 实现心跳机制的关键是 IdleStateHandler, 那么这个 Handler 如何使用呢? 先看下它的构造器：

```aspectj
public IdleStateHandler(int readerIdleTimeSeconds, int writerIdleTimeSeconds, int allIdleTimeSeconds) {
    this((long)readerIdleTimeSeconds, (long)writerIdleTimeSeconds, (long)allIdleTimeSeconds, TimeUnit.SECONDS);
}
```

这里解释下三个参数的含义：

+   readerIdleTimeSeconds: 读超时. 即当在指定的时间间隔内没有从 Channel 读取到数据时, 会触发一个 READER\_IDLE 的 IdleStateEvent 事件.
+   writerIdleTimeSeconds: 写超时. 即当在指定的时间间隔内没有数据写入到 Channel 时, 会触发一个 WRITER\_IDLE 的 IdleStateEvent 事件.
+   allIdleTimeSeconds: 读/写超时. 即当在指定的时间间隔内没有读或写操作时, 会触发一个 ALL\_IDLE 的 IdleStateEvent 事件.

> 注：这三个参数默认的时间单位是秒。若需要指定其他时间单位，可以使用另一个构造方法：IdleStateHandler(boolean observeOutput, long readerIdleTime, long writerIdleTime, long allIdleTime, TimeUnit unit)

在看下面的实现之前，建议先了解一下IdleStateHandler的实现原理。

下面直接上代码，需要注意的地方，会在代码中通过注释进行说明。

**使用IdleStateHandler实现心跳**

下面将使用IdleStateHandler来实现心跳，Client端连接到Server端后，会循环执行一个任务：**随机等待几秒**，**然后**ping**一下**Server**端**，**即发送一个心跳包**。当等待的时间超过规定时间，将会发送失败，以为Server端在此之前已经主动断开连接了。代码如下：

**Client端**

**ClientIdleStateTrigger —— 心跳触发器**

类ClientIdleStateTrigger也是一个Handler，只是重写了userEventTriggered方法，用于捕获IdleState.WRITER\_IDLE事件（未在指定时间内向服务器发送数据），然后向Server端发送一个心跳包。

```pf
/**
 * <p>
 *  用于捕获{@link IdleState#WRITER_IDLE}事件（未在指定时间内向服务器发送数据），然后向<code>Server</code>端发送一个心跳包。
 * </p>
 */
public class ClientIdleStateTrigger extends ChannelInboundHandlerAdapter {

    public static final String HEART_BEAT = "heart beat!";

    @Override
    public void userEventTriggered(ChannelHandlerContext ctx, Object evt) throws Exception {
        if (evt instanceof IdleStateEvent) {
            IdleState state = ((IdleStateEvent) evt).state();
            if (state == IdleState.WRITER_IDLE) {
                // write heartbeat to server
                ctx.writeAndFlush(HEART_BEAT);
            }
        } else {
            super.userEventTriggered(ctx, evt);
        }
    }

}
```

**Pinger —— 心跳发射器**

```java
/**
 * <p>客户端连接到服务器端后，会循环执行一个任务：随机等待几秒，然后ping一下Server端，即发送一个心跳包。</p>
 */
public class Pinger extends ChannelInboundHandlerAdapter {

    private Random random = new Random();
    private int baseRandom = 8;

    private Channel channel;

    @Override
    public void channelActive(ChannelHandlerContext ctx) throws Exception {
        super.channelActive(ctx);
        this.channel = ctx.channel();

        ping(ctx.channel());
    }

    private void ping(Channel channel) {
        int second = Math.max(1, random.nextInt(baseRandom));
        System.out.println("next heart beat will send after " + second + "s.");
        ScheduledFuture<?> future = channel.eventLoop().schedule(new Runnable() {
            @Override
            public void run() {
                if (channel.isActive()) {
                    System.out.println("sending heart beat to the server...");
                    channel.writeAndFlush(ClientIdleStateTrigger.HEART_BEAT);
                } else {
                    System.err.println("The connection had broken, cancel the task that will send a heart beat.");
                    channel.closeFuture();
                    throw new RuntimeException();
                }
            }
        }, second, TimeUnit.SECONDS);

        future.addListener(new GenericFutureListener() {
            @Override
            public void operationComplete(Future future) throws Exception {
                if (future.isSuccess()) {
                    ping(channel);
                }
            }
        });
    }

    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        // 当Channel已经断开的情况下, 仍然发送数据, 会抛异常, 该方法会被调用.
        cause.printStackTrace();
        ctx.close();
    }
}
```

**ClientHandlersInitializer —— 客户端处理器集合的初始化类**

```scala
public class ClientHandlersInitializer extends ChannelInitializer<SocketChannel> {

    private ReconnectHandler reconnectHandler;
    private EchoHandler echoHandler;

    public ClientHandlersInitializer(TcpClient tcpClient) {
        Assert.notNull(tcpClient, "TcpClient can not be null.");
        this.reconnectHandler = new ReconnectHandler(tcpClient);
        this.echoHandler = new EchoHandler();
    }

    @Override
    protected void initChannel(SocketChannel ch) throws Exception {
        ChannelPipeline pipeline = ch.pipeline();
        pipeline.addLast(new LengthFieldBasedFrameDecoder(Integer.MAX_VALUE, 0, 4, 0, 4));
        pipeline.addLast(new LengthFieldPrepender(4));
        pipeline.addLast(new StringDecoder(CharsetUtil.UTF_8));
        pipeline.addLast(new StringEncoder(CharsetUtil.UTF_8));
        pipeline.addLast(new Pinger());
    }
}
```

> 注： 上面的Handler集合，除了Pinger，其他都是编解码器和解决粘包，可以忽略。

**TcpClient —— TCP连接的客户端**

```csharp
public class TcpClient {

    private String host;
    private int port;
    private Bootstrap bootstrap;
    /** 将<code>Channel</code>保存起来, 可用于在其他非handler的地方发送数据 */
    private Channel channel;

    public TcpClient(String host, int port) {
        this(host, port, new ExponentialBackOffRetry(1000, Integer.MAX_VALUE, 60 * 1000));
    }

    public TcpClient(String host, int port, RetryPolicy retryPolicy) {
        this.host = host;
        this.port = port;
        init();
    }

    /**
     * 向远程TCP服务器请求连接
     */
    public void connect() {
        synchronized (bootstrap) {
            ChannelFuture future = bootstrap.connect(host, port);
            this.channel = future.channel();
        }
    }

    private void init() {
        EventLoopGroup group = new NioEventLoopGroup();
        // bootstrap 可重用, 只需在TcpClient实例化的时候初始化即可.
        bootstrap = new Bootstrap();
        bootstrap.group(group)
                .channel(NioSocketChannel.class)
                .handler(new ClientHandlersInitializer(TcpClient.this));
    }

    public static void main(String[] args) {
        TcpClient tcpClient = new TcpClient("localhost", 2222);
        tcpClient.connect();
    }

}
```

**Server端**

**ServerIdleStateTrigger —— 断连触发器**

```pf
/**
 * <p>在规定时间内未收到客户端的任何数据包, 将主动断开该连接</p>
 */
public class ServerIdleStateTrigger extends ChannelInboundHandlerAdapter {
    @Override
    public void userEventTriggered(ChannelHandlerContext ctx, Object evt) throws Exception {
        if (evt instanceof IdleStateEvent) {
            IdleState state = ((IdleStateEvent) evt).state();
            if (state == IdleState.READER_IDLE) {
                // 在规定时间内没有收到客户端的上行数据, 主动断开连接
                ctx.disconnect();
            }
        } else {
            super.userEventTriggered(ctx, evt);
        }
    }
}
```

**ServerBizHandler —— 服务器端的业务处理器**

```java
/**
 * <p>收到来自客户端的数据包后, 直接在控制台打印出来.</p>
 */
@ChannelHandler.Sharable
public class ServerBizHandler extends SimpleChannelInboundHandler<String> {

    private final String REC_HEART_BEAT = "I had received the heart beat!";

    @Override
    protected void channelRead0(ChannelHandlerContext ctx, String data) throws Exception {
        try {
            System.out.println("receive data: " + data);
//            ctx.writeAndFlush(REC_HEART_BEAT);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    @Override
    public void channelActive(ChannelHandlerContext ctx) throws Exception {
        System.out.println("Established connection with the remote client.");

        // do something

        ctx.fireChannelActive();
    }

    @Override
    public void channelInactive(ChannelHandlerContext ctx) throws Exception {
        System.out.println("Disconnected with the remote client.");

        // do something

        ctx.fireChannelInactive();
    }

    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        cause.printStackTrace();
        ctx.close();
    }
}
```

**ServerHandlerInitializer —— 服务器端处理器集合的初始化类**

```scala
/**
 * <p>用于初始化服务器端涉及到的所有<code>Handler</code></p>
 */
public class ServerHandlerInitializer extends ChannelInitializer<SocketChannel> {

    protected void initChannel(SocketChannel ch) throws Exception {
        ch.pipeline().addLast("idleStateHandler", new IdleStateHandler(5, 0, 0));
        ch.pipeline().addLast("idleStateTrigger", new ServerIdleStateTrigger());
        ch.pipeline().addLast("frameDecoder", new LengthFieldBasedFrameDecoder(Integer.MAX_VALUE, 0, 4, 0, 4));
        ch.pipeline().addLast("frameEncoder", new LengthFieldPrepender(4));
        ch.pipeline().addLast("decoder", new StringDecoder());
        ch.pipeline().addLast("encoder", new StringEncoder());
        ch.pipeline().addLast("bizHandler", new ServerBizHandler());
    }

}
```

> 注：new IdleStateHandler(5, 0, 0)该handler代表如果在5秒内没有收到来自客户端的任何数据包（包括但不限于心跳包），将会主动断开与该客户端的连接。

**TcpServer —— 服务器端**

```java
public class TcpServer {
    private int port;
    private ServerHandlerInitializer serverHandlerInitializer;

    public TcpServer(int port) {
        this.port = port;
        this.serverHandlerInitializer = new ServerHandlerInitializer();
    }

    public void start() {
        EventLoopGroup bossGroup = new NioEventLoopGroup(1);
        EventLoopGroup workerGroup = new NioEventLoopGroup();
        try {
            ServerBootstrap bootstrap = new ServerBootstrap();
            bootstrap.group(bossGroup, workerGroup)
                    .channel(NioServerSocketChannel.class)
                    .childHandler(this.serverHandlerInitializer);
            // 绑定端口，开始接收进来的连接
            ChannelFuture future = bootstrap.bind(port).sync();

            System.out.println("Server start listen at " + port);
            future.channel().closeFuture().sync();
        } catch (Exception e) {
            bossGroup.shutdownGracefully();
            workerGroup.shutdownGracefully();
            e.printStackTrace();
        }
    }

    public static void main(String[] args) throws Exception {
        int port = 2222;
        new TcpServer(port).start();
    }
}
```

至此，所有代码已经编写完毕。

**测试**

首先启动客户端，再启动服务器端。启动完成后，在客户端的控制台上，可以看到打印如下类似日志：

![img](https://img-blog.csdnimg.cn/img_convert/643f0d34252dcbcd2a351cb25fe3f2cb.png)

客户端控制台输出的日志

在服务器端可以看到控制台输出了类似如下的日志：

![img](https://img-blog.csdnimg.cn/img_convert/015d27b22ba65c80cab56c25609dea9f.png)

服务器端控制台输出的日志

### 43、默认情况 Netty 起多少线程？何时启动？

如果你在简历上写了Netty，那么面试官百分之九十的可能会问你Netty默认其多少线程？在什么时候启动的问题。

面试官一方面是想考验你对Netty有没有最基本的知识点掌握，一方面是想试探你有没有深入了解过Netty的[源码](https://so.csdn.net/so/search?q=%E6%BA%90%E7%A0%81&spm=1001.2101.3001.7020)和启动流程。

你在编写Netty服务端的时候经常会编写下面的代码：

```java
EventLoopGroup boss = new NioEventLoopGroup();
EventLoopGroup worker = new NioEventLoopGroup();

```

这里构建了两个事件循环组，循环组具体是干什么的我就暂时不细说了。我们拿其中的一个来进行分析底层的源码即可。这里调用了无参的构造方法，也就使用了默认的线程数，那么默认线程数是多少呢？慢慢进行分析：

```java
public NioEventLoopGroup() {
    this(0);
}

```

调用了“this(0)”，也就是调用了单个参数的构造方法，然后调用的传递线程数是0。

```java
public NioEventLoopGroup(int nThreads) {
    this(nThreads, (Executor) null);
}

```

紧接着调用 线程数和线程池接口的方法，需要注意的是，这里的“executor”是null。

```java
public NioEventLoopGroup(int nThreads, Executor executor) {
    this(nThreads, executor, SelectorProvider.provider());
}

```

因为Netty底层封装了NIO所以调用了传递“provider”的构造参数。

```java
public NioEventLoopGroup(int nThreads, Executor executor, final SelectorProvider selectorProvider) {
    this(nThreads, executor, selectorProvider, DefaultSelectStrategyFactory.INSTANCE);
}

```

紧接着比之前的多了一个默认选择策略工厂，传递了一个单例对象。

```java
public NioEventLoopGroup(int nThreads, Executor executor, final SelectorProvider selectorProvider, final SelectStrategyFactory selectStrategyFactory) {
    super(nThreads, executor, selectorProvider, selectStrategyFactory, RejectedExecutionHandlers.reject());
}

```

之后调用了父类的构造方法，这里又比之前多了一个参数是异常拒绝处理器，也就是出现异常的时候执行的拒绝处理器。

```java
protected MultithreadEventLoopGroup(int nThreads, Executor executor, Object... args) {
    super(nThreads == 0 ? DEFAULT_EVENT_LOOP_THREADS : nThreads, executor, args);
}

```

紧接着又调用了父类的“MultithreadEventLoopGroup”构造方法，下面这个就是默认初始化的线程了：

```java
nThreads == 0 ? DEFAULT_EVENT_LOOP_THREADS : nThreads

```

这里是一个三元表达式，判断传递过来的参数“nThreads”是否等于0，如果是的话就赋值“DEFAULT\_EVENT\_LOOP\_THREADS”，如果不是的话就赋值为传递过来的值。

那么“DEFAULT\_EVENT\_LOOP\_THREADS”是在什么时候初始化的呢？是在静态代码块中初始化。

```java
private static final int DEFAULT_EVENT_LOOP_THREADS;
static {
    DEFAULT_EVENT_LOOP_THREADS = Math.max(1, SystemPropertyUtil.getInt(
            "io.netty.eventLoopThreads", NettyRuntime.availableProcessors() * 2));

    if (logger.isDebugEnabled()) {
        logger.debug("-Dio.netty.eventLoopThreads: {}", DEFAULT_EVENT_LOOP_THREADS);
    }
}

```

它获取的值也就是“NettyRuntime.availableProcessors() \* 2”。

然后调用了“availableProcessors”的方法：

```java
public static int availableProcessors()
{
    return holder.availableProcessors();
}

synchronized int availableProcessors() {
    if (this.availableProcessors == 0) {
        final int availableProcessors =SystemPropertyUtil.getInt(
                        "io.netty.availableProcessors",
                        Runtime.getRuntime().availableProcessors());
        setAvailableProcessors(availableProcessors);
    }
    return this.availableProcessors;
}

```

需要注意的就是“Runtime.getRuntime().availableProcessors()”这个方法，这个方法的意思是获取运行时可用线程数。接下来下来写个方法测试一下：

```java
public class NettyServer {
    public static void main(String[] args) {
        System.out.println(Runtime.getRuntime().availableProcessors());
    }
}

```

由此可见，Netty的默认启动了电脑可用线程数的两倍，在调用了bind方法的时候执行。

```auto
“Runtime.getRuntime().availableProcessors()”
```

那么反过来思考下！

我们真的需要每个EventLoopGroup都默认启用线程吗？

答案当然不是！

我们具体的线程数应该交由业务来决定而不是使用默认的参数。

有的时候我们只需要使用一个线程来监听注册事件。

比如，在客户端代码中， 线程数的调整，非常有必要。

### 44、聊聊：NioEventLoopGroup 默认的构造函数会起多少线程？

同上

### 45、聊聊：如何设计一个内存池，或者内存分配器

> 这是出现的次数比较多的大厂面试题：怎样设计一个内存池和内存分配器？
>
> 尼恩暗语：会的人不多，如果能答上来，面试官会两眼发绿光

**重要性：对内存分配器透彻理解，并且具备实操能力，是编程高手的标志之一**。

如果你不能理解malloc之类内存分配器实现原理的话，那你可能就写不出高性能程序，写不出高性能程序就很难参与核心项目，参与不了核心项目那么很难升职加薪，很难升级加薪就无法走向人生巅峰，所以， 内存分配非常关键

说明：此题是一个实操性质的题目，后续尼恩带大家参考netty内存池，从0到1，架构、设计、实现一个高性能内存池组件

### 46、聊聊：如何设计一个Java对象池，减少GC和内存分配消耗

**重要性：对对象池透彻理解，并且具备实操能力，也是编程高手的标志之一**。

对象池顾名思义就是存放对象的池，与我们常听到的线程池、数据库连接池、http连接池等一样，都是典型的池化设计思想。

对象池的优点就是可以集中管理池中对象，减少频繁创建和销毁长期使用的对象，从而提升复用性，以节约资源的消耗，可以有效避免频繁为对象分配内存和释放堆中内存，进而减轻jvm垃圾收集器的负担，避免内存抖动。

Apache Common Pool2 是Apache提供的一个通用对象池技术实现，可以方便定制化自己需要的对象池，大名鼎鼎的 Redis 客户端 Jedis 内部连接池就是基于它来实现的。

说明：此题是一个实操性质的题目，后续尼恩带大家参考netty对象池，从0到1，架构、设计、实现一个高性能对象池组件

### 参考文献

https://segmentfault.com/a/1190000022568931

https://blog.csdn.net/MonkeyBrothers/article/details/122860753

https://blog.csdn.net/kaihuishang666/article/details/116095480

http://www.wjhsh.net/hujinshui-p-10450548.html

https://blog.csdn.net/crazymakercircle/article/details/124588880