
# 第 15 章 Linux 网络

连接关闭：远程主机断开连接。

另一个可以从网络远程计算机获取 shell 的工具是`login`。该工具是多种`"r"`工具之一，允许在不指定密码的情况下访问网络远程系统；`rcp`工具用于在计算机之间拷贝文件，`rsh`工具用于在远程计算机上执行命令。

`"r"`工具允许在无密码的情况下访问远程计算机，前提是远程计算机设置了信任访问。设置信任访问的一种方法是将计算机的主机添加到远程计算机的`/etc/hosts.equiv`中；以下`/etc/hosts.equiv`允许登录到`www.sampledomain.com`和`www.sampledomain2.com`计算机的用户使用`login`、`rcp`和`rsh`工具以相同用户身份连接计算机，无需指定密码：

```
[root@localhost]# cat /etc/hosts.equiv

www.sampledomain.com

www.sampledomain2.com

[root@localhost]#
```

如果用户`mary`使用`www.sampledomain.com`登录远程计算机并使用`"r"`连接本地计算机，她将自动使用本地`mary`账户登录系统，无需指定密码。在拥有相同用户账户的多个`Linux`服务器的公司中，这种访问是不可安全的；设置信任访问允许登录一台`Linux`计算机的用户访问其他计算机，而无需重新输入密码。

另一种设置信任访问的方法是在想要使用信任访问的每个用户的本地计算机家目录下创建一个`.rhosts`文件。考虑以下`/home/mary/.rhosts`：

```
[root@localhost]# cat /home/mary/.rhosts

www.sampledomain.com

www.sampledomain2.com

[root@localhost]#
```

这将允许`www.sampledomain.com`和`www.sampledomain2.com`计算机上的`mary`用户使用`"r"`工具以`mary`用户身份连接到本地计算机，无需指定密码。此外，`/root/.hosts`文件可以允许其他信任计算机上的`root`用户使用`"r"`工具连接到本地计算机，无需指定密码。

## 连接到网络资源

假设远程计算机`remoteserver`已经设置了信任访问；您可以使用以下命令获取一个`shell`：

```
[root@localhost root]# rlogin remoteserver

Last login: Thu Aug 15 13:16:51 from 100.6.6.0

You have new mail.

[root@localhost]# _
```

同样，您可以使用以下命令从计算机`remoteserver`拷贝将`/etc/hosts`文件复制到本地计算机：

```
[root@localhost]# rpc remoteserver:/etc/hosts localhost:/root

[root@localhost]# ls -F /root

Desktop/ hosts

[root@localhost]# _
```

此外，若要在`remoteserver`计算机上运行`who`命令并将结果显示在本地终端，您可以使用以下命令：

```
[root@localhost root]# rsh remoteserver who

root tty2 Aug 15 12:26

root pts/0 Aug 15 13:16 (100.6.6.0)

[root@localhost]# _
```

> 今天，`rsh`和`login`命令可能被`ssh`（安全`shell`）命令取代；该命令通过加密网络上计算机之间的通信来增强安全性。

## 访问电子邮件

回想第 1 章，网络用户可以使用多种邮件用户代理（`MUA`）程序从电子邮件服务器获取电子邮件。电子邮件通常通过`POP`（邮局协议）或`IMAP`（交互式邮件访问协议）从电子邮件服务器下载。`POP`通常将邮件消息从电子邮件服务器下载到客户端计算机，而`IMAP`通常将邮件消息留在电子邮件服务器上并在跨网络进行查看。无论从电子邮件服务器发送邮件到邮件用户代理时使用何种方法，邮件都会通过`SMTP`（简单邮件传输协议）从邮件用户代理发送到电子邮件服务器。必要服务器的地址应在邮件用户程序的相应值中配置。

`Red Hat Linux`中最常用的邮件用户代理是`Mozilla`，它还可以充当`Web`浏览器、`FTP`客户端和新闻组阅读器。若要打开`Mozilla`，只需使用鼠标点击`KDE`或`GNOME`桌面工具栏上的`Mozilla`图标即可。打开后，导航到“任务”（`Tasks`）菜单并选择“邮件”（`Mail`）：如果没有配置任何邮件账户，将出现图 15-19 所示的向导。

**图 15-19 配置新的电子邮件账户**

从图 15-19 中选择“`ISP`或电子邮件提供商”（`ISP or email provider`）并点击“下一步”按钮，将提示您输入用户名、`POP/IMAP`、`SMTP`和账户信息，如图 15-20、15-21、15-22 和 15-23 所示。

**图 15-20 指定用户信息**

**图 15-21 配置 POP、IMAP 和 SMTP 服务器**

**图 15-22 指定用户名**

**图 15-23 指定账户名（继续-修正）**

一旦配置了服务器和账户信息，导航到“任务”菜单并选择“邮件”，将弹出图 15-24 所示的`Mozilla`邮件用户代理，用于发送和接收电子邮件消息。

**图 15-24 Mozilla 电子邮件客户端**

## 常见网络服务

回想第 1 章，`Linux`为网络上的用户提供了各种服务。这些服务通常由一组守护进程（`daemon processes`）表示，这些进程在网络上监听某些请求。守护进程通过只监听具有特定数字的封包来识别它们要响应的数据包；这个数字被称为“端口”（`port`），它唯一标识一个特定服务。端口及其协议定义在`/etc/services`文件中；若要查看`telnet`守护进程监听哪个端口，您可以使用以下命令：

```
[root@localhost root]# grep telnet /etc/services

telnet 23/tcp

telnet 23/udp

telnet 107/tcp # 远程 Telnet

telnet 107/udp

tokens 992/tcp

tokens 992/udp

[root@localhost root]#
```

上述输出表明`telnet`守护进程同时使用`TCP/IP`和`UDP`协议监听端口`23`。端口范围从`0`到`65535`。端口`0–1023`称为“良性端口”，因为它们代表了常用服务。此外，网络工具可能会直接连接到提供网络服务的守护进程，也可能通过互联网守护进程（`inetd`）连接到守护进程，如图 15-25 所示。

**图 15-25 与网络服务的交互**

互联网守护进程通常用于启动和管理较小守护进程的连接，例如`telnet`和`FTP`守护进程。它在启动时自动启动并使用`/etc/inetd.conf`；通常，此文件包含了`/etc/inetd.d`目录下所有以守护进程命名的文件；例如，`telnet`守护进程是由互联网守护进程通过`/etc/inetd.d/telnet`文件进行配置的，如下输出所示：

```
[root@localhost root]# cat /etc/inetd.d/telnet

# description: The telnet 服务器提供 telnet 会话；它使用未加密的用户名/密码对进行认证。

{

    flags = REUSE

    socket_type = stream

    wait = no

    user = root

    server = /usr/sbin/telnet

    log_on

    [root@localhost root]#
```
