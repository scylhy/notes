### 01-HTTP初探

1989年蒂姆·伯纳斯·李提出在互联网上构建超链接文档系统的构想（级world wide web），并确立三项关键技术：
1. URI:统一资源标识符，作为互联网资源的唯一身份
2. HTML:超文本标记语言，描述超文本文档
3. HTTP:超文本传输协议，用来传输超文本  

http/0.9采用纯文本格式，只允许“Get”动作，从服务器上获取html文档，相应请求后关闭连接，功能有限。它是一个简单的文本协议，只能获取文本资源。

http/1.0  
NCSA（美国国家超级计算应用中心）1993年开发出Mosaic（第一个可以图文混排的浏览器），1995年开发出了服务器软件Apache，简化了HTTP服务器的搭建工作。  
随后出现了JPEG图像格式、MP3音乐格式 
http/1.0在1996年正是发布（不是标准，不具有实际约束力），和如今的HTTP差别不大：
1. 增加了HEAD、POST等新方法
2. 增加了响应状态码、标记可能的错误原因
3. 引入了协议版本号概念
4. 引入了HTTP Header(头部)的概念，让HTTP处理请求和响应更灵活
5. 传输数据不再仅限于文本

http/1.1是正是标准，发布于1999年：
1. 增加了PUT、DELETE等新的方法
2. 增加了缓存管理和控制
3. 明确了连接管理，允许持久连接
4. 允许响应数据分开（chunked)，利于传输大文件
5. 强制要求Host头，让互联网主机托管成为可能

http/1.1是目前互联网上使用最广泛的协议，功能非常完善。

Google开发了自己的浏览器，并推出了新的SPDY协议，并把SPDY推上标准，HTTP/2充分考虑了如今互联网的现状：宽带、移动、不安全
http/2主要特点：
1. 二进制协议，不再是纯文本
2. 可发起多个请求，废弃了1.1里的管道
3. 使用专用算法压缩头部，减少数据传输量
4. 允许服务器主动客户端推送数据
5. 增强了安全性，事实上要求加密通信
http/2基于Google的SPDY协议，注重性能改善，但还未普及。


http/3基于Google的QUIC进入标准指定阶段，是未来的发展方向




put、delete在restful应用里，表示对资源的操作。http很灵活，也有一些历史一流问题，不必强求什么特性都用上。


笔记来源：极客时间，透视HTTP协议

---

### 02-HTTP是什么

HTTP即超文本传输协议，涉及超文本、传输、协议

HTTP是一个用在计算机世界里的协议。它使用计算机能够理解的语言确立计算机之间交流通信的规范，以及相关的各种控制和错误处理方式。  

HTTP是一个在计算机世界里专门用来在两点之间传输数据的规定和规范。 不能用于广播、寻址或路由。
双向传输协议，允许中继   

HTTP是一个在计算机世界里专门在两点之间传输文字、图片、音频、视频等超文本数据的约定和规范。  


HTTP不是一个孤立的协议，它是构建互联网的基础技术，它没有实体、依赖许多其他技术来实现，但同时许多技术也都依赖于它。



---

### 03-HTTP全览  


网络世界是什么样的？实例的互联网是有许许多多个规模略小的网络连接而成的。

*浏览器*本质上是一个HTTP协议中的请求方。在HTTP协议里，浏览器的角色被称为“User Agent"即用户代理，简称客户端。

*Web服务器*，是HTTP里的应答方（响应方），有硬件和软件两层含义。

*Apache老牌服务器*，Nginx是Web服务器里的后期之后，特点是高性能、高稳定、易于扩展。  

**Apache/Nginx应该叫做HTTP服务器，而Tomcat应该叫做应用服务器。**  

*CDN*，全程“Content Delivery Network"，内容分发网络，应用了HTTP协议的混存和代理技术，代理源站响应客户端的请求。
除了基本的网络加速外，还提供负载均衡、安全防护、边缘计算、跨运行上网络等功能。  

*爬虫*，另一种用户代理，“机器人”，实际上是一种可以自动访问Web资源的应用程序。  

据估计，互联网上至少有50%的流量都是有爬虫产生的。 只用服务器和带宽，影响网站数据分析，容器导致敏感信息泄漏。  
*反爬虫技术*，君子协定，robots.txt，规定哪些可以爬，哪些不可以爬。


HTML/WebService/WAF  

HTML有HTML4和5两个主要标准，广义上的HTML指HTML、JS、CSS等前段技术的组合。

WebService，是一种由w3c定义的应用服务器开发规范，使用client-server主从架构，通常使用wsdl定义服务结构，使用http协议传输xml或soap消息，即它是一种基于Web(http)的服务架构技术。

因为采用了HTTP协议传输数据，所以WebSercie架构里服务器和客户端可以采用不同的操作系统和语言开发，具有异构性。

WAF，网络应用防火墙，应用层面的防火墙，专门监测HTTP流量，是防护web应用的安全技术。

---

### 04-与HTTP相关的各种协议  


TCP/IP是事实上的标准通信协议，是一系列网络通信协议的同城。


IP协议、TCP协议、DNS、URI/URL、HTTPS、代理

URI=协议名（http）+主机名(nginx.org)+路径（/en/download.html）

HTTPS(HTTP over SSL/TLS)=http+ssl//tls+tpc/ip

SSL（Secure Socket Layer）有网景公司发明，发展到3.0时被标准化，改名为TLS(Transprot Layer Security),由于历史的原因，很多成称之为SSL/TLS或者直接成为SSL

代理：匿名代理、透明代理、正向代理、反向代理。

CDN也是一种代理，替代源站响应客户端请求，通常扮演这透明代理和反向代理的角色。

HTTP还有一个特殊的代理协议，有指明的代理软件HAproxy指定，但不是RFC标准。


