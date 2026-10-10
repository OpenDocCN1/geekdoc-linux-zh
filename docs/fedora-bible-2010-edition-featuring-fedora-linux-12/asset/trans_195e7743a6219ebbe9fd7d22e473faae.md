

## 网络信息系统服务器

网络信息系统（NIS）是由 Sun Microsystems 开发的一个软件功能，用于管理网络上的一组 UNIX（以及现在的 Linux）计算机所需的配置信息。使用 NIS，一组计算机可以共享通用的 passwd、groups、hosts 以及其他配置文件。

默认情况下，NIS 服务是关闭的。您可以将 Linux 计算机的 NIS 服务作为 NIS 客户端（使用共享信息）或 NIS 服务器（分发共享信息）开启。NIS 客户端计算机需要启动 `/etc/init.d/ypbind` 脚本，并在 `/etc/yp.conf` 文件中指定 NIS 服务器。

若要将 Fedora 用作 NIS 服务器，您必须收集想要共享的配置文件，然后启动 `/etc/init.d/ypserv` 脚本。该脚本运行 `/usr/sbin/ypserv` 守护进程，该守护进程负责向 NIS 客户端计算机分发信息。

## 动态主机配置协议服务器

您无需逐一到本地网络中的每台计算机添加其正常工作所需的所有 TCP/IP 信息（IP 地址、子网掩码、网关等），而是可以将 Fedora 配置为动态主机配置协议（DHCP）服务器来分发这些信息。客户端计算机只需识别 DHCP 服务器的 IP 地址，这样当客户端启动其网络连接时，DHCP 服务器就会自动为其分配网络地址。

默认情况下，DHCP 是关闭的。要开启它，请输入 `chkconfig dhcpcd on`。然后通过输入 `service dhcpcd start` 启动该服务。除了启动服务外，您还必须配置 `/etc/dhcpd.conf` 文件。

> 交叉引用：第 22 章描述了如何设置 DHCP 服务器。

## 轻量级目录访问协议服务器

如果您的组织使用轻量级目录访问协议（LDAP）信息数据库，运行随 Fedora 提供的 LDAP 服务器可让您访问这些数据库。同样，LDAP 服务器还能让您使用支持 LDAP 的应用程序，例如 Thunderbird、Evolution 以及其他可以共享 LDAP 服务器通讯录的应用程序。

默认情况下，LDAP 服务是关闭的。要开启它，请输入 `chkconfig ldap on`。要启动该服务，请输入 `service ldap start`。除了运行启动脚本外，您还必须配置 `/etc/ldap/` 目录中的文件。

> 交叉引用：第 21 章展示了如何使用 LDAP 设置电子邮件通讯录。

## 域名系统服务器

域名系统（DNS）服务器用于在 TCP/IP 网络中将主机名转换为 IP 地址。可以使用 named 守护进程将 Fedora 配置为 DNS 服务器。

默认情况下，Fedora 中的 DNS 服务器未配置为自动启动。在启动服务之前，您必须配置 /etc/named.conf 文件并配置区域文件（位于 /var/named 目录中）。要开启 DNS 服务器，请输入 `chkconfig named on`。要启动该服务，请输入 `service named start`。

## 反向地址解析协议服务器

反向地址解析协议（RARP）守护进程响应来自必须获取自身 IP 地址的 RARP 客户端的请求。如今，RARP 已很少使用。

默认情况下，RARP 软件包（rarpd）未被安装。安装后，服务是关闭的。要开启 RARP 服务器，请输入 `chkconfig rarpd on`。要启动该服务，请输入 `service rarpd start`。当地址请求进来时，`/usr/sbin/rarpd` 守护进程会检查 `/etc/ethers` 或 NIS 数据库中的地址。

## 数据库服务

数据库服务器提供用于访问和管理信息数据库的工具。PostgreSQL 服务使用 postmaster 守护进程来处理其服务请求。MySQL 服务器运行 mysqld 守护进程来处理对其数据库的访问。这些守护进程从 `/etc/init.d` 中的启动脚本启动：分别是 postgresql 和 mysqld 脚本。

许多其他数据库也在 Linux 上运行，包括 Firebird 等开源数据库以及 Oracle 和 DB2 等商业产品。

> **交叉引用：** 第 23 章描述了如何设置 MySQL 数据库服务器。

## 用户服务

Fedora 可以为最终用户提供各种网络服务。这些服务允许用户实时发送消息并获取活动用户的信息。

### Talk 服务器

使用 in.talk 或 in.ntalk 服务器允许用户通过 talk 命令进行通信。talk 命令允许用户实时来回输入消息。talk 守护进程处理端口 517 上的请求，而 ntalk 守护进程处理端口 518 上的请求。

这两种服务默认都是关闭的。要开启任一服务，请编辑 `/etc/xinetd.d/talk` 和/或 `/etc/xinetd.d/ntalk` 文件，并将 `disable = yes` 条目更改为 `disable = no`。然后重启 xinetd 守护进程：`service xinetd restart`。

### Finger 服务器

`finger`（`/usr/sbin/in.fingerd`）服务器允许人们使用 `finger` 命令请求有关本地或通过网络在 Linux 或 UNIX 系统上活动用户的信息。此服务默认是关闭的。如果 `in.fingerd` 服务器接受了来自 `finger` 命令的请求，则向发出请求的用户输出的内容大致如下：

```
[maple]
Login: jake
Name: Jake W. Jones
Directory: /home/jake
Shell: /bin/bash
Last login Mon May 12 13:34 (PDT) on pts/2 from maple
Mail last read Mon May 12 12:10 2008 (PDT)
```

输出显示用户的登录名、真实姓名、主目录和 shell。它还显示用户最后一次登录以及访问其电子邮件的时间。

**注意：** 由于此服务会暴露个人或组织信息，您可能不希望将 finger 服务开放到公共网络上。

### 远程用户识别

`rusers` 服务器（`/usr/sbin/rpc.ruserd`）允许用户从远程计算机查询系统，以列出当前登录到 Fedora 系统的用户。可以使用 `rusers` 命令来查询 `rpc.ruserd` 服务器。

默认情况下，`rusers` 服务是关闭的。要启动服务器，请输入 `chkconfig ruserd on`。要立即启动该服务，请输入 `service ruserd start`。与 `finger` 服务一样，`rusers` 很少应该暴露给公共网络。

### 向所有用户写入服务器

向所有用户写入（Write-to-All，`rwall`）服务器（`/usr/sbin/rpc.rwalld`）接受请求以向当前登录到 Fedora、RHEL 或其他 UNIX 系统的所有用户的屏幕广播文本消息。该请求通过 `rwall` 命令发出。默认情况下，`rwall` 服务是关闭的。要启动 `rwall` 服务器，请输入 `chkconfig rwalld on`。要启动该服务，请输入 `service xinetd start`。

### 安全服务

Fedora 提供一些服务来保护您的本地网络免受外部攻击。这些服务包括系统日志记录、虚拟专用网络服务器和缓存服务器。以下章节描述了这些服务。

### 系统日志记录

虽然系统日志记录设施（`rsyslog` 软件包）并非专门的网络服务，但它会记录计算机上大多数网络服务（以及其他服务）的信息和错误消息。系统日志记录守护进程（`/sbin/rsyslogd`）应该始终处于运行状态。

默认情况下，`rsyslogd` 守护进程在所有多用户运行级别（2、3、4 和 5）下启动。您可以通过重新配置 `/etc/rsyslog.conf` 文件来更改记录的消息或将日志记录消息定向到不同的文件。您可以通过编辑 `/etc/sysconfig/rsyslog` 文件来更改 `rsyslogd` 守护进程使用的选项。

### 虚拟专用网络服务器

通过对在公共网络上传输的数据进行加密，虚拟专用网络（VPN）可以为用户提供一种从远程位置访问本地网络的安全方式。Fedora 包含 openswan 软件包，该包用于提供 IPsec VPN 服务。Fedora 还包含 openvpn，这是一种 SSL VPN 服务，并且包括使用 openssh 支持通过 TUN/TAP 网络接口进行隧道技术的能力。

> **交叉引用：** 有关 IPsec 的更多信息，请参见第 15 章。

### 代理/缓存服务器

Squid 服务器（`/usr/sbin/squid`）既可以用作代理服务器，也可以用作缓存服务器。代理服务器可以通过将所有请求通过代理服务器传递，从而允许本地网络上的计算机与 Internet 通信。缓存服务器将本地用户访问过的 Web 内容存储在物理上比源计算机更接近用户的计算机上。

默认情况下，Squid 服务器是关闭的。要启动 Squid 服务器，请输入 `chkconfig squid on`。要安装 squid，请输入 `yum install squid`。

要启动该服务，请输入 `service squid start`。您还必须设置 `/etc/squid/squid.conf` 文件以识别谁有权访问服务器以及他们可以访问哪些服务。

> **交叉引用：** 第 15 章提供了配置 Squid 的详细信息。

### 网络服务参考

表 B-1 提供了有关特定网络服务的详细信息。

