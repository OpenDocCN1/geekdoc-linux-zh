
# 技巧 | 窍门 | 黑客手段 | 应用程序

![](img/30dc0459712b32ede1a3814d456b41b6_39_0.png)

## 06 rcdc 实用程序

rcdc 可执行文件是名称服务器控制实用程序。它控制名称进程的操作，并通过 TCP 连接与 named 进程进行通信。rcdc 实用程序拥有一个名为 rcdc.conf 的配置文件，其结构和语法与 named.conf 相似。您可以输入 `man rcdc-confgen` 和 `man rcdc.conf` 以获取更多信息。

![](img/30dc0459712b32ede1a3814d456b41b6_39_1.png)

## 07 其他类型的 DNS 服务器

还有另外三种类型的 DNS 服务器：主服务器、从服务器和转发服务器。每个域名至少应有一个主 DNS 服务器和一个从 DNS 服务器。

主 DNS 服务器（或 Master）定义了一个或多个区域文件，该 DNS 服务器对这些区域具有权威性。区域是通过 NS 资源记录分配给 DNS 服务器的。

从 DNS 服务器（Slave）主要充当主 DNS 服务器的备份，以防其因某种原因宕机。

转发 DNS 服务器从客户端的角度来看与缓存服务器几乎相同。其区别在于它本身不执行递归查询；它只是将查询转发到另一个 DNS 服务器，获取响应，然后缓存结果。

无法从查询结果中判断它是从区域主服务器还是从服务器获得回答的。

## 08 /etc/bind 目录

所有与 BIND 相关的配置文件都位于 /etc/bind 目录内。您需要 root 访问权限才能对其进行修改，并且必须重启 named 进程以使更改生效。

BIND 在 `/var/cache/bind` 目录内保存其他一些文件：

```bash
$ ls -l /var/cache/bind/
total 24
-rw-r--- 1 bind bind 698 Oct 15 09:46 managed-keys.bind
-rw-r--- 1 bind bind 512 Oct 15 09:46 managed-keys.bind.jnl
-rw-r--- 1 bind bind 9446 Oct 15 11:17 named_dump.db
-rw-r--- 1 bind bind 1103 Oct 14 19:58 named.stats
```

![](img/30dc0459712b32ede1a3814d456b41b6_39_2.png)

## 09 /etc/bind/db.root 文件

db.root 文件保存了根名称服务器（由单个点表示）的信息，这些信息用于初始化互联网域名服务器的缓存。您可以通过运行以下命令手动生成它：

```bash
$ dig @root-servers.net . NS > db.root
```

## 10 配置文件

默认的 BIND 配置几乎已准备好支持缓存 DNS 服务器。您只需要显式开启递归，一切就完成了。此操作可以通过在 `named.conf.options` 内部添加一行包含 `recursion yes;` 文本的内容来完成。

接下来的步骤是运行 BIND 服务器进程，如下所示：

```bash
# /etc/init.d/bind9 start
```

您还需要添加访问控制列表以减少流量并提高安全性，您将在稍后的步骤 16 中更多了解访问控制列表。DNS 服务通常监听端口 53，您从以下输出中可以清楚地看到：

```bash
$ telnet localhost 53
Trying ::1..
Connected to localhost.
```

## 11 管理缓存 DNS 服务器

您已经知道如何启动 DNS 服务器。以下命令将其停止：

```bash
# /etc/init.d/bind9 stop
```

然后，此命令将其重启：

```bash
# /etc/init.d/bind9 restart
[ ... ] Stopping domain name service...
bindingwaiting for pid 24713 to die
[ ok ] Starting domain name service...
bind9.
```

![](img/30dc0459712b32ede1a3814d456b41b6_40_0.png)

就本教程而言，最有用的实用程序是 **named-checkconf**，它检查配置的正确性。如果当前配置中没有语法错误，您将不会得到任何输出。没有工具能捕捉逻辑上的 DNS 错误。

![](img/30dc0459712b32ede1a3814d456b41b6_40_1.png)

> BIND 的所有日志消息都存储在 /var/log/syslog 中

## 12 使用缓存 DNS 服务器

缓存服务器像普通 DNS 服务器一样使用。如果您想减少局域网上的 DNS 流量，应将缓存服务器的 IP 放入 */etc/resolv.conf* 文件中，并注释掉所有其他 DNS 服务器。然而，这可能很危险，因为如果缓存 DNS 服务器因某种原因停止工作，您的网络将无法正常运行。

![](img/30dc0459712b32ede1a3814d456b41b6_40_2.png)

```bash
host -t ns linuxuser.co.uk linode
;; connection timed out; no servers can be contacted
rMacBook:Downloads mtsouk$ host -t ns linuxuser.co.uk linode
Using domain server:
Name: linode
Address: 109.74.193.253#53
Aliases:

linuxuser.co.uk name server ns.hosteurope.com.
linuxuser.co.uk name server ns2.hosteurope.com.
$ host -t ns linuxuser.co.uk linode
Using domain server:
Name: linode
Address: 109.74.193.253#53
Aliases:

Host linuxuser.co.uk not found: (SERVFAIL)
```

## 13 BIND 的日志文件

BIND 的所有日志消息都存储在 */var/log/syslog* 文件中。**named** 命令可能会产生大量的日志消息，因此您可能会决定在确保 DNS 服务器无问题运行后，使用 **rndc** 降低日志级别。

## 14 访问控制列表 (ACL)

ACL 列表定义了哪些主机可以或不可以访问 DNS 服务器。以下行定义了一个新的访问控制列表：

```
acl OIENET {
    2.86/16;
    localhost;
    localnets;
};
```

列表的定义不会自动激活该列表。您应该添加以下行以启用 OIENET 访问控制列表：

```
allow-query { OIENET; };
```

一旦 DNS 服务器开始运行，许多未知主机会尝试连接；因此，不要延迟生成所需的访问列表以保护您的 DNS 服务器。

## 15 检查您的配置

BIND 附带了许多可以帮助您检查当前配置正确性的工具。这些工具包括 **named-checkconf**、**named-checkzone** 和 **named-compilezone**。

## 16 测试缓存 DNS 服务器

为了测试您的 DNS 服务器，请尝试查询一个不在 DNS 缓存中的域名，并查看回答该查询需要多少时间。接下来，再次询问同一 DNS 服务器，您应该看到响应时间明显变好。

![](img/30dc0459712b32ede1a3814d456b41b6_40_3.png)

## 17 缓存服务器的优势

在网络上使用缓存 DNS 服务器的优点是减少局域网流量和互联网流量。对于已经被缓存服务器回答过的查询，您也能更快地获得 DNS 响应。

BIND 有一个方便的命令，可以将 DNS 服务器的所有记录转储到单个文件中。启动时它还可以重新读取这些数据：

```bash
# rndc dumpdb -all
# ls -l /var/cache/bind/named_dump.db
-rw-r--r-- 1 bind bind 9448 Oct 15 11:15 /var/cache/bind/named_dump.db
```

# 技巧 | 窍门 | 黑客手段 | 应用程序

## 编程客户端-服务器应用程序

每个操作系统都提供其自己的网络 API 集合，但 Qt 提供了一个简化创建“爱说话”应用程序的解决方案

![](img/30dc0459712b32ede1a3814d456b41b6_41_0.png)

**现代计算机网络由多种协议组成。** 手工创建格式正确的数据包几乎是不可能的——协议栈及其底层网络硬件会影响格式。

**在 Unix 上工作的工程师**通过引入一个抽象层解决了这个问题——所谓的**套接字**充当两个本地或远程应用程序之间的端点。开发人员使用标准化接口向套接字发出命令，这些命令随后被翻译到网络中。

处理套接字时，具备基本的网络知识是有好处的。目前，只需定义消息可以通过两种高级协议传输即可。

**TCP** – 传输控制协议的缩写 – 在数据成功交付时提供确认。这是通过相对复杂的数据包序列实现的，这增加了通信过程的开销。然而，某些应用并不要求这一点。对于这些应用，**UDP** 提供了一种更简洁的通信协议，放弃了交付确认。在网络中，计算机通过其 IP 地址来识别。单独的服务然后通过其端口号来识别 – 可以将它们视为高层建筑内部的公寓门牌号。

**从事通信软件开发的开发人员**往往面临先有鸡还是先有蛋的局面 – 如果没有编写服务器，客户端就无法连接。另一方面，缺少客户端意味着服务器无法测试。

在实际项目中，您应该首先创建客户端和服务器将交换的消息的粗略模型。不需要第一次就做到 100% 正确；大多数协议在实现过程中会发生变化。

我们的指法练习级应用程序不需要这种级别的复杂性。只需从创建一个名为 ImagineITCPServer 的命令行项目开始就足够了。Qt Creator 不会将网络模块添加到新创建的应用程序中。这可以通过打开其 .pro 文件并调整 QT 指令以在编译时包含网络来轻松解决。

```
QT += network
```

这样一来，就该创建服务器对象了。其声明可以放在负责程序启动的 main() 函数内部：

```cpp
myServer=new QTcpServer();
if(myServer->listen(QHostAddress::Any, 1025)==false)
{
        qDebug() << "Server error" << myServer->serverError();
        return 0;
}
else
{
        qDebug() << "Server up" << myServer->serverAddress() << " ";
        myServer->serverPort();
}
```

在经典的 Berkeley 套接字编程中，服务器和客户端逻辑由套接字类的实例处理。Qt 提供了一个专用服务器，其中包含用于连接管理的辅助方法。启动后，我们调用 listen() 方法以使我们的 QTcpServer 等待传入连接。

