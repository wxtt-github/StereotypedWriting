## 计算机网络面试题

#### 1.HTTP 1.0和2.0有什么区别？

**HTTP/1.0版本主要增加了以下几点：**

1. 增加了HEAD、POST等新方法
2. 增加了响应状态码
3. 引入了头部，即请求头和响应头
4. 在请求中加入了HTTP版本号
5. 引入了Content-Type，使得传输的数据不再局限于文本

**HTTP/1.1版本主要增加了以下几点：**

1. 增加了连接管理即keepalive，允许持久连接
2. 支持pipeline，无需等待前面的请求响应，即可发送第二次请求
3. 允许响应数据分块(chunked)，即响应的时候不标明Content-Length，客户端就无法断开连接，直到收到服务端的EOF，利于传输大文件
4. 新增了缓存的控制和管理
5. 加入了Host头，用在当一台机子部署了多个主机，然后多个域名解析又是同一个IP，此时加入了Host头就可以判断你到底是要访问哪个主机

**HTTP/2版本主要增加了以下几点：**

1. 是二进制协议，不再是纯文本
2. 支持一个TCP连接发起多请求，移除了pipeline
3. 利用HPACK压缩头部，减少数据传输量
4. 允许服务端主动推送数据

**扩展知识：HTTP从发明到3.0的演进之路**

1969年，互联网的始祖-阿帕网(ARPA)，成功建立

1974年，ARPA的罗伯特·卡恩和斯坦福的文顿·瑟夫提出TCP/IP协议

1990年，蒂姆·伯纳斯-李(李老)创建了运行万维网所需的所有工具：超文本传输协议(HTTP)、超文本标记语言(HTML)、第一个网页浏览器、第一个网页服务器和第一个网站

至此，互联网开启了快速发展之路。

**HTTP/0.9时代**

1989年，李老发表了一篇论文，提出了三个概念:

1. URL(uniform resource locator)，统一资源标识符，作为互联网上的唯一标识
2. HTML(hyper-text markup langurage)，超文本标记语言，用于描述超文本
3. HTTP(hyper-text transfer protocol)，超文本传输协议，用于传输超文本

**HTTP/1.0时代**

需求促使添加各种特性来满足用户的需求，经过一系列草案，HTTP/1.0于1996年正式发布

1. 增加了HEAD、POST等新方法
2. 增加了响应状态码
3. 引入了头部，即请求头和响应头
4. 在请求中加入了HTTP版本号
5. 引入了Content-Type，使得传输的数据不再局限于文本

**HTTP/1.1时代**

更新主要是因为HTTP/1.0很大的性能问题，就是每请求一个资源都得新建一个TCP连接，而且只能串行请求，因此在HTTP/1.1版本主要增加以下几点：

1. 增加了连接管理即keepalive，允许持久连接
2. 支持pipeline，无需等待前面的请求响应，即可发送第二次请求
3. 允许响应数据分块(chunked)，即响应的时候不标明Content-Length，客户端就无法断开连接，直到收到服务端的EOF，利于传输大文件
4. 新增了缓存的控制和管理
5. 加入了Host头，用在当一台机子部署了多个主机，然后多个域名解析又是同一个IP，此时加入了Host头就可以判断你到底是要访问哪个主机

**HTTP/2时代**

HTTP/1.1发布后，互联网开始了爆发式的增长，这同时暴露出HTTP的不足，主要还是性能问题，在2015年发布了HTTP/2，主要增加了以下几点：

1. 是二进制协议，不再是纯文本
2. 支持一个TCP连接发起多请求，移除了pipeline
3. 利用HPACK压缩头部，减少数据传输量
4. 允许服务端主动推送数据

**HTTP/3时代**

这次的痛点来自于HTTP依赖的TCP，TCP是面向可靠的、有序的传输协议，而HTTP/2是所有流共享一个TCP连接，所以会有TCP层面的队头阻塞，当发生重传时会影响多个请求响应，并且TCP是基于四元组(源IP，源端口，目的IP，目的端口)来确定连接的，而在移动网络的情况下IP地址会频繁更换，这会导致反复的建连。而且还有TCP与TLS的叠加握手，增加了延时。

因此Google就研究出了基于UDP的QUIC协议。2018年，互联网标准化组织IETF提议将HTTP over QUIC更名为HTTP/3并获得批准。

#### 2.HTTP 2.0和3.0有什么区别？

1. 基于的传输层协议不同

- HTTP/2：基于TCP，使用二进制分帧层实现多路复用
- HTTP/3：基于UDP，使用QUIC(Quick UDP Internet Connections)协议，提供类似TCP的可靠性和多路复用

2. 性能区别

- HTTP/2：解决了HTTP/1.x中的队头阻塞问题，但仍然受制于TCP的队头阻塞，尤其在高延迟或丢包情况下
- HTTP/3：通过QUIC协议，避免了TCP队头阻塞，即使在网络不稳定的情况下也能提供更好的性能

3. 从安全性的角度

- HTTP/2：可以使用TLS加密(HTTPS)，但加密并非强制要求
- HTTP/3：默认使用QUIC自带的TLS 1.3加密，安全性更高，且加密是强制的

4. 从连接建立速度：

- HTTP/2：需要TCP三次握手和TLS握手，连接建立相对较慢
- HTTP/3：QUIC集成了连接建立和加密握手，连接建立速度更快，尤其在初次连接时

#### 3.常见的HTTP状态码有哪些？

每个状态码由三位数字组成，第一位数字表示类别，常见的HTTP状态码分为五大类。

1）1xx：信息响应

- 100 Continue：服务器已接收请求的初步部分，客户端应继续请求
- 101 Switching Protocols：服务器同意切换协议，如从HTTP切换到WebSocket

2）2xx：成功

- 200 OK：请求成功，服务器返回所请求的资源或数据
- 201 Created：请求成功并创建了新的资源，常用于POST请求
- 204 No Content：请求成功但服务器不返回任何内容，常用于删除操作

3）3xx：重定向

- 301 Moved Permanently：资源已永久移动到新的URL，客户端应使用新URL访问
- 302 Found：资源临时移动到新的URL，客户端应继续使用原来的URL
- 304 Not Modified：资源未修改，客户端可以使用缓存版本
- 307 Temporary Redirect：与302 Found类似，但要求客户端必须使用相同的HTTP方法进行重定向请求，保证重定向的语义一致性

4）4xx：客户端错误

- 400 Bad Request：请求无效或语法错误，服务器无法处理
- 401 Unauthorized：请求需要身份验证，客户端未提供有效的凭证
- 403 Forbidden：服务器理解请求但拒绝执行，通常是权限问题
- 404 Not Found：请求的资源在服务器上未找到

5）5xx：服务器错误

- 500 Internal Server Error：服务器内部错误，无法完成请求
- 502 Bad Gateway：服务器作为网关或代理，从上游服务器收到无效响应
- 503 Service Unavailable：服务器暂时无法处理请求，通常是因为过载或维护

#### 4.HTTP请求包含哪些内容，请求头和请求体有哪些类型？

**HTTP请求由以下几部分组成：**

1. 请求行（Request Line）：包含请求方法（如GET、POST）请求的资源路径（如/index.html）、以及HTTP协议版本（如HTTP/1.1）
2. 请求头（Request Headers）：包含各种键值对，用于传递客户端环境、请求内容、认证信息等
3. 空行（Blank Line）：用于分隔请求头和请求体
4. 请求体（Request Body）：仅在POST、PUT等方法中存在，包含需要发送到服务器的数据

**常见的请求头类型：**

1. 通用头部（General Headers）：适用于请求和响应，如Cache Control、Connection等
2. 请求头部（Request Headers）：特定于请求的头部，如Host、User-Agent、Accept、Authorization等
3. 实体头部（Entity Headers）：描述请求体的头部，如Content-Type、Content-Length

**请求体的类型：**

1. 表单数据（Form Data）：application/x-www-form-urlencoded，用于提交表单数据
2. 多部份数据（Multipart Data）：multipart/form-data，用于上传文件或复杂表单数据
3. JSON数据：application/json，用于提交JSON格式的数据
4. XML数据：application/xml，用于提交XML格式的数据
5. 文本数据：text/plain，用于提交纯文本数据

#### 5.HTTP和HTTPS有什么区别？

**回答：**

1）数据传输安全性：

- HTTP：数据以明文传输，容易被窃听、篡改
- HTTPS：通过SSL/TLS协议对数据进行加密传输，提供数据机密性和完整性保障

2）端口号：

- HTTP：默认使用端口号80
- HTTPS：默认使用端口号443

3）性能：

- HTTP：无加密过程，连接建立速度稍快
- HTTPS：基于HTTP上又加了SSL（Secure Sockets Layer）或TLS（Transport Layer Security）协议来实现的加密传输，加解密过程增加了计算开销，握手时间较长，但现代硬件和协议优化已使性能差距减小

4）SEO影响：

HTTP：搜索引擎一般会降低未加密站点的排名

HTTPS：搜多引擎更倾向于优先展示HTTPS网站

**扩展知识**





























































