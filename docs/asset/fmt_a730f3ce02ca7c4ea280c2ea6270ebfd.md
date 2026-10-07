
- * E22.8 使用 `tcpdump` 捕获活动和被动会话的流量。FTP 对你的安全有什么影响？

- * E22.9 下列 `iptables` 规则允许什么？

```bash
Chain INPUT (policy ACCEPT)
target source RELATED,ESTABLISHED
ACCEPT tcp anywhere state NEW dpt:www
ACCEPT tcp anywhere state NEW dpt:ssh
DROP all
```

```bash
Chain FORWARD (policy ACCEPT)
target source destination
```

- * E22.10 检查本地规则。讨论你发现了什么。是否存在漏洞？（需要 root 权限。）

- * E22.11 编写一个确定网络接口是否处于混杂模式的工具。在你的网络中定期运行它以快速发现入侵。该工具产生多大的负载？你必须在每台机器上运行它，还是可以远程运行？

# 23 托管

今天，UNIX 和 Linux 系统是提供 Web 内容和应用程序的主流平台。它们是执行此任务的理想系统，因为它们从一开始就被设计为抢占多任务系统。它们能够处理大量的 Web 请求，并且高效、安全可靠。

在某些方面，基于 Web 的应用程序实际上简化了系统管理员的工作。“Web 2.0”特性如 AJAX（异步 JavaScript 和 XML）为用户带来了本地安装应用程序的功能和响应，同时也减轻了管理员大量的部署烦恼。

在服务器端，LAMP（Linux、Apache、MySQL 和 PHP/Perl/Python）栈是一种常见的配置，而且功能强大。对于数据库驱动的应用程序，Ruby on Rails 是一个基于 Ruby 语言的流行 Web 框架。这两个栈都是合理的选择且易于支持。

- 1. 非 Linux UNIX 发行版将此集合简单称为 "AMP"。Solaris 用户称之为 "SAMP"，而 Windows 用户称之为 "WAMP"，真是不可思议。

## 23.1 Web 托管基础

托管网站与提供其他网络服务并没有本质区别。一个守护进程在 TCP 端口 80（HTTP 标准）上监听连接，接收文档请求，并将其传输到请求用户的浏览器。这些文档中的许多是结合数据库和应用程序框架动态生成的，但这与底层的 HTTP 协议无关。

### Web 上的资源位置

互联网上的信息按照一个由互联网学会（ISOC）定义的架构进行组织。这个初衷良好（尽管带有委员会色彩）的组织有助于确保整个互联网的一致性和互操作性。

ISOC 定义了识别资源的三种主要方式：统一资源标识符 (`URIs`)、统一资源定位符 (`URLs`) 和统一资源名称 (`URNs`)。`URL` 和 `URN` 实际上是 `URI` 的特殊类型，如附 A 所示。

### 图 A 统一资源分类法

![](img/f9b22d506ca334ae9c37c1129906a270_1004_0.png)

区别是什么？

- URL 通过描述其主要的访问机制（例如 `http://admin.com`）告诉你如何定位资源。
- URN 识别（“命名”）资源，但不暗示其位置或告诉你如何访问它（例如 `urn:isbn:0-13-020601-6`）。

什么时候称某物为 URI？如果资源只能通过互联网访问，请将其称为为 URL。如果它可以通过互联网或其他手段访问，那么你正在使用 URI。

### 统一资源定位符

大多数时候，你处理的是 URL，它通过五个基本组件描述了如何访问对象：

- 协议或应用程序
- 主机名
- TCP/IP 端口（可选）
- 目录（可选）
- 文件名（可选）

## 第 23 章 Web 托管

表 23.1 显示了可以在 URL 中使用的一些协议。

### 表 23.1 URL 协议

| 协议 | 作用 | 示例 |
|---|---|---|
| file | 访问本地文件 | `file:///etc/syslog.conf` |
| ftp | 通过 FTP 访问远程文件 | `ftp://ftp.admin.com/adduser.tar.gz` |
| http | 通过 HTTP 访问远程文件 | `http://admin.com/index.html` |
| https | 通过 HTTP/SSL 访问远程文件 | `https://admin.com/order.shtml` |
| ldap | 访问 LDAP 服务 | `ldap://ldap.bigfoot.com:389/cn=Herb` |
| mailto | 向指定地址发送电子邮件 | `mailto:linux@book.admin.com` |

### HTTP 如何工作

HTTP 是一个无状态的客户端/服务器协议。客户端向服务器请求特定 URL 的“内容”。服务器返回一段数据或某种类型的错误消息。客户端可以继续请求另一个对象。

由于 HTTP 非常简单，你可以通过运行 `telnet` 来变成一个代码 Web 浏览器。只需连接到你选择的 Web 服务器的 80 端口即可。

最常用的命令是 `GET`，它请求文档的内容。通常 `GET /` 是你想要的，因为它请求你所连接的任何服务器的根文档（通常是首页）。HTTP 是大小敏感的，请确保用大写字母输入命令。

```
$ telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.atrust.com.
Escape character is '^'.
GET /\n<此处出现你的默认文件的内容>
Connection closed by foreign host.
```

一个更“完整”的 HTTP 请求将包含 HTTP 协议版本、请求针对的主机（从名称虚拟主机检索文件所必需）以及其他信息。响应将包含信息性标头以及响应数据。例如：

```
$ telnet localhost 80
Trying 127.0.0.1...
Connected to localhost.atrust.com.
Escape character is '^'.
GET / HTTP/1.1
Host: www.atrust.com
HTTP/1.1 200 OK
Date: Sat, 01 Aug 2009 17:43:10 GMT
Server: Apache/2.2.3 (CentOS)
```

### FastCGI

Last-Modified: Sat, 01 Aug 2009 16:20:22 GMT

Content-Length: 7044

Content-Type: text/html

```
<此处出现你的默认文件的内容>
Connection closed by foreign host.
```

在这种情况下，我们告诉服务器我们将使用 HTTP 协议版本 1.1，并指明了我们请求信息的虚拟主机。服务器返回了状态码（HTTP/1.1 200 OK）、它认为的当前日期和时间、它运行的服务器软件名称和版本、请求文件的最后修改日期、请求文件的长度以及请求文件的内容类型。标头信息通过空行与内容隔开。

### 动态内容生成

除了提供静态文档外，HTTP 服务器还可以为用户提供动态创建的内容。例如，如果你想提供当前的时间温度，CGI 并不是一种编程语言，而是 HTTP 服务器与其他程序交换信息的规范。这种神奇的技巧是 CGI，通常用 Perl、Python 或 PHP 编写。

## 负载均衡

像 Java 这样功能完备的语言。Java 应用与企业或其他数据源接口的常用方法是使用“servlet”。

Servlet 是运行在应用程序服务器平台之上的 Java 程序。应用程序服务器可以独立运行，也可以与 Apache 协同工作。大多数应用程序服务器是由程序员为程序员设计的，缺乏系统管理员所期望的简洁调试机制。表 23.3 突出了一些常用的 UNIX/Linux 应用程序。

## 表 23.3 应用程序

| 服务器 | 类型 | 网站 |
| :--- | :--- | :--- |
| Tomcat | 开源 | tomcat.apache.org |
| GlassFish | 开源 | glassfish.dev.java.net |
| JBoss | 开源 | jboss.org |
| OC4J | 商业 | oracle.com/technology/tech/java/oc4j |
| WebSphere | 商业 | lbm.com/websphere |
| WebLogic | 商业 | oracle.com/appserver/weblogic/webologic-suite.html |
| Jetty | 开源 | eclipse.org/jetty |

如果你面临着支持这些应用程序服务器之一的情况，请寻找特定产品的文档和培训。相信我们，这种技术并不是你通过大多数 UNIX 和 Linux 应用就能“随手学会”的。你已经收到过警告了。

## 负载均衡

要预测服务器在单位时间内能处理多少次命中（对象请求，包括图像）或页面访问（HTML 页面请求）是非常的。服务器的容量取决于系统的硬件架构（包括子系统）、其运行的操作系统、已执行任何系统调优的程度和重点，可能最重要的是正在构建的网站结构。（它们包含静态 HTML 页面，还是必须进行数据库调用和数值计算？）

只有通过在实际硬件上对你的实际网站进行直接的基准测试和测量，才能回答“多少命中？”这个问题。有时，在相似硬件上构建过类似网站的人可以提供对规划非常有帮助的信息。在任何情况下，都不应该相信系统供应商提供的数字。还要记住，带宽也是一个关键考虑因素。一台为单个客户端提供 HTML 文件和图像的机器可以轻松提供足够的数据来饱和 OC3 (155 Mb/s) 链路。

与其关注扩展性，一个更好的关注参数是可扩展性；Web 服务器通常在饱和其以太网接口之前变成 CPU-IO 限制。确保你和你的 Web 设计团队计划将高流量网站的负载分散到多个服务器上。

## 第 23 章

## Web 托管

负载均衡同时增加了性能和冗余。有几种不同的负载均衡方法可用：轮询 DNS、负载均衡硬件和基于软件的负载均衡器。

有关 DNS 及其行为的更多信息请第 17 章。

轮询 DNS 是负载均衡最简单、最原始的格式。在这个系统中，多个 IP 地址被分配给单个主机。当对网站 IP 地址的请求到达名称服务器时，客户端接收其中一个 IP 地址作为响应。地址一个接一个地、按照重复的“轮询”顺序发放。

轮询负载均衡非常常见。Google 甚至在使用它。例如，如果你查询 `www.google.com` 的 DNS 基础设施，你可能会得到类似下面的记录：

```
$ dig www.google.com a

;; QUESTION SECTION:
;; www.google.com.      IN A

;; ANSWER SECTION:
www.google.com.      0 IN CNAME   www.l.google.com.
www.google.com.      65 IN A      74.125.95.104
www.google.com.      65 IN A      74.125.95.105
www.google.com.      65 IN A      74.125.95.106
www.google.com.      65 IN A      74.125.95.147
www.google.com.      65 IN A      74.125.95.99
www.google.com.      65 IN A      74.125.95.103
```

在这个示例中，名称 `www.google.com` 映射到规范名称 `www.l.google.com`。Google 添加了这一层间接，以便它可以将内容交付的责任委托给如 Akamai 等下游提供商（更多背景请参见第 978 页的的内容分发网络），而不必赋予 CDN 对其根域名的控制权。

DNS 客户端可以选取 `www.google.com` 返回的任何 A 记录；它应该是随机执行的。与普遍认为相反，第一个记录的顺序并不是“主要的”。因为客户端是随机选择地址，所以该网站的负载大致均匀分布在这些服务器上。

轮询 DNS 的问题在于，如果一台服务器宕机，必须更新 DNS 数据以将流量路由离开。A 记录上的长超时使得此操作变得复杂且不可靠。另一方面，短超时会阻碍缓存，并使你网站的 DNS 查询变慢且消耗更多资源。第 556 页有关于这种权衡的缓存和效率描述。

在示例中，A 记录可以在过期前缓存 65 秒。这是一个相对短的超时。如果你有备用服务器，你可能倾向于为 A 记录使用更长的超时，并简单将禁用服务器的 IP 地址重新分配给备用服务器。

## 选择服务器

负载均衡硬件是轮询 DNS 的简单替代方案，但它需要专门设备。可以使用基于软件的均衡器。

- 负载均衡硬件
- 基于软件的负载均衡器
- 轮询 DNS
- 负载均衡硬件
- 基于软件的负载均衡器
- 轮询 DNS
- 负载均衡硬件
- 基于软件的负载均衡器
- 轮询 DNS
- 负载均衡硬件
- 基于软件的负载均衡器
- 轮询 DNS
- 负载均衡硬件
- 基于软件的负载均衡器

## 选择服务器

这里是你可能想要考虑的一些因素：

- 健壮性
- 性能
- 更新的及时性
- 支持级别
- 成本
- 访问控制和安全
- 作为代理的能力
- 处理加密的能力

## 表 23.4 Apache 的位置

| 系统 | 目录 | 推荐的二进制文件来源 |
| :--- | :--- | :--- |
| Linux | `/usr/sbin` | 标准发行版 |
| Solaris | `/usr/apache2` | 标准发行版 |
| HP-UX | `/opt/apache` | 安装 HP-UX 11i Web Suite |
| AIX | `/usr/IBM` | 安装 HTTPServer |

## 安装 Apache

如果你决定下载 Apache 源码并自行编译，请从发行版包含的 `configure` 脚本开始。该脚本会自动检测系统类型并设置 Makefile。使用 `--prefix` 选项来指定 Apache 服务器在目录树中的位置。例如：

```
$ ./configure=/etc/httpd/
```

如果你没有指定 prefix，默认值为 `/usr/local/apache2`。

你可以使用 `configure --help` 查看所有可能的参数的列表，大部分参数由 `--enable-module` 和 `--disable-module` 选项组成，用于包含或排除 Web 服务器内部各种功能组件。

你还可以通过指定选项 `--enable-module=shared` 将模块编译为动态共享对象文件（或使用 `--enabled-mods=all` 包含所有模块）。这样，只有在 `httpd` 配置中指定的模块会在运行时加载。这实际上是二进制版 Apache 包的默认配置——所有模块都编译成共享对象，并在 Apache 启动时动态加载。

## 配置 Apache

有关标准模块的完整列表，请参阅 `httpd.apache.org/docs-2.2/mod`。

虽然默认的模块集是合理的，但你可能也想启用表 23.5 所示的模块。

### 表 23.5 默认未用的 Apache 模块

| 模块 | 功能 |
| --- | --- |
| authn_dbm | 使用 数据库管理用户/组访问（如果你需要对网站的某些区域进行基于密码的用户级访问，建议使用此项） |
| rewrite | 使用正则表达式重写 URL |
| expires | 允许你为文档附加过期日期 |
| proxy | 将 Apache 作为代理服务器使用 |
| mod_ssl | 对 HTTPS 的安全套接层（SSL）的支持 |

> a. s. 也称为传输层安全协议（TLS）；请参见第 971 页。

同样，你可能也想禁用表 23.6 列出的模块。出于安全和性能考虑，禁用你确定认为不会使用的模块是一个好主意。

### 表 23.6 我们建议移除的 Apache 模块

| 模块 | 功能 |
| --- | --- |
| asis | 允许发送指定类型的文件而不带 HTTP 头部 |
| autoindex | 显示没有默认 HTML 文件的目录内容 |
| env | 允许为 CGI 脚本设置特殊的环境变量 |
| userdir | 允许用户拥有自己的 HTML 目录 |

当 `configure` 执行完毕后，运行 `make` 然后运行 `make install` 以实际编译并安装适当的文件。

遗憾的是，在 AIX 上编译 Apache 并不并不那么简单。请参阅 `people.apache.org/rawick/apache-on-aix.html` 中的技巧和技巧。

## 配置 Apache

一旦你安装了服务器，其配置文件将保存在安装目录的 `conf` 子目录中。检查并自定义 `httpd.conf` 文件，该文件分为三个部分。

第一部分涉及全局设置，例如服务器池、HTTP 服务器监听查询的 TCP 端口（通常是 80 端口，尽管你可以选择其他端口——而且，你可以在单台机器上通过不同的端口运行多个 HTTP 服务器）以及动态模块加载的设置。

## 第 23 章 Web 托管

第二部分配置“默认”服务器，即处理任何未由 `VirtualHost`（虚拟主机）定义响应的服务器（参见第 971 页）。该部分的配置参数包括运行服务器的用户和组（root 以外的用户！）以及至关重要的 `DocumentRoot` 设置，它定义了提供文档的目录树根节点。该部分还处理诸如“特殊”URL 的处理，例如使用 `~user` 语法访问用户主目录的 URL。
