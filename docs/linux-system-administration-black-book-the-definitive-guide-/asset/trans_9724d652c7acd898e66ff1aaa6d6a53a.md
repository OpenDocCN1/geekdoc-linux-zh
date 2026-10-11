
- FastCGI——FastCGI 模块并不随 Apache 服务器附带提供。但可以在 www.fastcgi.com 获取。
- Java——如果你有现有的 Java 代码，计划将其包含在网站上，或者你的客户希望使用 Java，那你走运了。Java 用户可能对 Jakarta 感兴趣，这是一个开源的 Java 服务器解决方案项目，位于 http://jakarta.apache.org。另外，位于 http://java.apache.org 的 Java Apache 项目也值得关注。
- mSQL 身份验证——如果你希望使用 mSQL 进行数据库身份验证，Apache 可以支持此功能。
- PHP——Apache 支持 PHP 服务器端脚本语言。有关此工具及其功能的更多信息，请参阅 www.php.net。
- 密码身份验证——如果你需要为任何网页或网站强制登录，Apache 支持此功能。
- Perl——Perl 编程语言（在第 21 章中有介绍）受 Apache Web 服务器支持。有关此主题的更多信息，请访问 http://perl.apache.org。
- SSI——Apache 能够使用服务器端包含（SSI）以及扩展服务器端包含（xSSI）。
- SSL——安全套接字层（SSL）实现是加密应用程序，因此美国和某些其他政府将其视为军火。出于这个原因，SSL 支持不包含在主要的 Apache 发行版中。请访问 www.apache.org/related_projects.html 查看提供 Apache SSL 支持的机构列表，以及指向许多其他基于 Apache 的项目的指针。
- URL 重写——如果你需要操纵传入的 URL 并重定向它们，你可以在 Apache 中实现这一点。
- 虚拟主机——你可以使用 Apache 虚拟托管尽可能多的网站，具体数量取决于你的操作系统能处理多少。幸运的是，Linux 足够健壮，可以处理高 Web 负载。如果你遇到 Web 服务变慢的问题，请考虑为服务器增加更多 RAM。
- XML——一个专门的 Apache 项目团队致力于可扩展标记语言（XML）。请访问 http://xml.apache.org 了解更多关于 Apache XML 解决方案的信息。

### 模块

许多 Apache 功能是通过模块实现的。这是现代软件应用的常见特性。模块化程序通常包含一个核心，其中包含运行主程序所需的一切。模块本身各自包含特定功能或一组功能。如果你想使用包含在此模块中的功能，就将其添加到核心程序中。

13. Apache Web 服务器

模块化构建策略解决了程序功能繁多但导致机器变慢的问题，因为软件本身占用了你所有的 RAM。这有时被称为 *功能蔓延*。有关如何将功能模块插入服务器的信息，请参阅“配置 httpd”部分。

## 配置文件

曾经使用三个文件来配置 Apache Web 服务器：access.conf、httpd.conf 和 srm.conf。这些文件中的每一个都控制着服务器的特定方面或其功能。access.conf 文件提供安全控制。你可以使用此文件来开启或关闭服务器功能，或指定谁被允许访问你的 Web 服务的特定部分。如果你在同一台机器上运行互联网 Web 服务器和内联网 Web 服务器，你需要花一些时间来正确配置此文件。

httpd.conf 文件控制 httpd 本身。这里是你选择服务器加载的模块——功能片段——的位置，以及它记录什么和 httpd 的许多其他方面。最后，srm.conf 跟踪服务器所需的所有组件的位置。从服务器组件到 Web 页面位置，都在其中设置。

> 注意：*标准 Apache 安装将这些项目放置在 /usr/local/ 中，但 Red Hat 的安装将它们放置在 /etc/httpd/conf/ 中。*

从 Apache 版本 1.3 开始——作为 Red Hat 6.1 的更新 RPM 提供，并默认包含在 Red Hat 6.2 中——所有配置信息现在都在 httpd.conf 中。其他两个文件仍然存在，但只包含指向主文件的指针。每当阅读提及 access.conf 或 srm.conf 的文档时，你看到的是 Apache 1.2 及更早版本的文档。

Apache 访问文件允许你设置 Web 服务器安全的各个方面。此文件以一组描述性注释开始，然后转到以下内容：

```
ServerType standalone
```

> 注意：*我在代码出现的地方删除了大段注释，因为这些描述在文件本身中比显示在这本书中更有用。*

ServerType 声明设置 Apache 是运行自己的 httpd 实例还是让 inetd 处理传入请求。使用 standalone 会运行一个独立的守护进程，而使用 inetd 则通过超级守护程序处理。下一个指令也是与服务器相关的；它告诉 httpd 在哪里找到其配置、错误以及有时是日志文件：

ServerRoot /etc/httpd

可以将 ServerRoot 指令视为指向服务器除 Web 页面本身外所需的大部分信息。在服务器设置之后，紧接着是：

```
LockFile /var/lock/httpd.lock
```

LockFile 指令设置锁文件的默认路径，该锁文件用于防止子进程尝试处理已由另一个进程处理的传入请求。在此之后是另一个文件位置设置：

```
PidFile /var/run/httpd.pid
```

Apache 在一个由 PidFile 指令设置的特殊文件中跟踪其自身的进程 ID。在这种情况下，设置了文件的具体路径。你也可以使用从 ServerRoot 指定位置开始的相对路径。

ScoreBoardFile 设置了另一个特殊文件。Linux 操作系统需要一个文件在父服务器和其子进程之间传递信息。在这种情况下，ScoreBoardFile 设置为完整路径：

```
ScoreBoardFile /var/run/httpd.scoreboard
```

接下来两条陈述与之前 Apache 版本的配置方法相关：

```
#ResourceConfig conf/srm.conf
#AccessConfig conf/access.conf
```

> **注意：** *每行开头的井号符号导致 Apache 忽略此代码，因此将其注释掉。*

ResourceConfig 语句指向在服务器解析 httpd.conf 之后读取的 Apache 指令。AccessConfig 语句包含更多在 ResourceConfig 文件之后读取的指令。过去 Apache 就是这样操作的。现在，你开始涉及到不涉及文件的设置，例如：

```
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
```

这些与超时相关的指令在表 13.1 中有说明。

表 13.1 **在 /etc/httpd.conf 中可用的与超时及其他时间相关的指令。**

| 指令 | 用途 | 值 |
| :--- | :--- | :--- |
| **KeepAlive** | 启用或禁用全连接。 | **On** 或 **Off** |
| **KeepAliveTimeout** | 指定 Apache 在关闭连接前在请求之间等待多少秒。 | 秒数 |
| **MaxKeepAliveRequests** | 指定客户端在保持连接打开时可以发出的最大请求数。 | 请求数；值为 0 表示无限 |
| **Timeout** | 指定 Apache 在关闭连接前等待后续请求到达的秒数。 | 秒数 |

时间相关指令之后是进程相关指令：

```
MinSpareServers 8
MaxSpareServers 20
StartServers 10
MaxClients 150
MaxRequestsPerChild 100
```

此处列出的项目在表 13.2 中有进一步讨论。

接下来两条指令告诉 Apache 在何处监听传入连接：

```
#Listen 3000
#Listen 12.34.56.78:80
```

表 13.2 **在 /etc/httpd.conf 中可用的与进程相关的指令。**

| 指令 | 结果 |
| :--- | :--- |
| **MaxClients** | 指定此服务器将接受的同时 HTTP 请求的最大数量 |
| **MaxRequestsPerChild** | 指定子服务器在关闭前应处理的请求数 |
| **MaxSpareServers** | 指定你希望保留以等待额外 HTTP 请求的空闲子服务器的最大数量 |
| **MinSpareServers** | 指定你希望保留以用于额外 HTTP 请求的空闲子服务器的最小数量 |
| **StartServers** | 指定机器或 Apache 首次启动时创建的子服务器数量 |

