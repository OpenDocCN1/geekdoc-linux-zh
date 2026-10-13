
| G.ROOT-SERVERS.NET | 3600000 NS | G.ROOT-SERVERS.NET. |
| | 3600000 A | 192.112.36.4 |
- 曾名为 AOS.ARLY.ARM.MIL

| H.ROOT-SERVERS.NET | 3600000 NS | H.ROOT-SERVERS.NET. |
| | 3600000 A | 128.63.2.53 |
- 曾名为 NIC.NORDU.NET

| I.ROOT-SERVERS.NET. | 3600000 NS | I.ROOT-SERVERS.NET. |
| | 3600000 A | 192.36.148.17 |
| 由 Verisign, Inc. 运营 |

| J.ROOT-SERVERS.NET. | 3600000 NS | J.ROOT-SERVERS.NET. |
| | 3600000 A | 192.58.128.30 |
| 托管在 LINX，由 RIPE NCC 运营 |

| K.ROOT-SERVERS.NET. | 3600000 NS | K.ROOT-SERVERS.NET. |
| | 3600000 A | 193.0.14.129 |
| 由 IANA 运营 |

| L.ROOT-SERVERS.NET. | 3600000 NS | L.ROOT-SERVERS.NET. |
| | 3600000 A | 198.32.64.12 |
| 托管在日本，由 WIDE 运营 |

| M.ROOT-SERVERS.NET. | 3600000 NS | M.ROOT-SERVERS.NET. |
| | 3600000 A | 202.12.27.33 |
| 文件结束 |

此文件包含 NS 和 A 资源记录，指定了权威域名服务器的名称（在每条记录的第一字段用 `.` 表示）。

文件中的注释行以分号 `;` 开头。这些注释为您提供了关于根域名服务器位置的提示。互联网有 13 台根服务器；大多数根服务器位于美国。这对于任何域名服务器来说都是必须的，因为域名服务器必须能够访问到至少一个根域名服务器。

## `/var/named/localhost.zone` 文件

`/etc/named.conf` 文件包含一个针对 localhost 区域的区域语句，该语句指定文件名为 `.zone`。该文件位于您的 Red Linux 系统的 `/var/named` 目录下。以下是 `/var/named/localhost.zone` 文件的内容：

```
$TTL 86400
@ORIGIN localhost.
@ root ( : serial (d. adams)
42 : refresh
3H : retry
15M : expire
1W : expiry
1D ) : minimum
1D IN NS @
1D IN A 127.0.0.1
```

## 配置 DNS

此区域文件以 `$TTL` 指令开头，为未定义 TTL 的后续记录设置 TTL 为一天（86400 秒）。接下来，`$ORIGIN` 指令将域名设置为 localhost。

# 688 理解网络信息服务 (NIS)

当你成功使用 `dig` 访问 DNS 服务器时，你就可以通过请求该服务器执行的操作来反转位。例如，我输入以下命令来尝试对 IP 地址 192.168.0.2 进行反向查找：

```
host 192.168.0.2 localhost
```

该命令显示如下输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
```

```
2.0.168.192.in-addr.arpa domain name pointer wxp.
```

# 理解网络信息服务 (NIS)

网络信息服务（NIS）由太阳微系统（Sun Microsystems）开发，用于在局域网内的所有计算机之间共享信息。NIS 最常用的信息类型如下：

- 来自 `/etc/passwd` 和 `/etc/shadow` 文件的用户名和密码
- 来自 `/etc/group` 文件的组信息

通常，每个系统在各自的文件中有一份信息副本，任何更改都需要单独更新每个系统上的文件。使用 NIS，你可以在 NIS 服务器上为一组计算机维护一套配置文件。所有其他运行 NIS 客户端的计算机都可以访问这些文件。例如，如果你的用户名和密码在 NIS 数据库中，你将能够登录网络上所有运行 NIS 客户端程序的计算机。

![](img/509edf67e1a0798154916aafeb3f0878_715_0.png)

NIS 最初被称为 Sun Yellow Pages (YP)，但由于“Yellow Pages”一词是英国电信（British Telecom）在英国注册的商标，因此太阳系统不得不更改名称。这导致 NIS 的包名都以字母 `yp` 开头。

# NIS 如何工作

如果你想在网络中使用 NIS，必须将至少一台计算机设置为 NIS 服务器。你可以在网络中拥有多个 NIS 服务器，每台服务器为不同的计算机组提供服务。你也可以拥有一个主 NIS 服务器和一个或多个从 NIS 服务器，从服务器接收主服务器数据库的副本。主 NIS 服务器支持的计算机组被称为 NIS 域或 Y 域。

NIS 服务器运行 `ypserv` 守护进程（这是 NIS 的守护进程），它在 DBM 数据库中维护共享信息。（DBM 指数据管理，一类用于数据库中键值对的函数库）。NIS 数据库称为映射（maps）。你可以通过使用 NIS 服务器软件自带的 `/usr/lib/yp/ypmap` 程序直接通过文本配置文件（如 `/etc/passwd` 和 `/etc/group`）创建这些映射。更准确地说，`ypserv` 守护进程使用 `/var/yp` 目录下的 `Makefile` 为所有共享配置文件创建映射。

主 NIS 服务器向所有 NIS 客户端提供映射。客户端运行 `ypbind`，各种客户端程序通过它访问 NIS 服务器。除了主服务器，还可以设置一个或多个从服务器，在主服务器不可用或宕机时提供 NIS 映射。NIS 服务器定期从主服务器复制映射（使用 `/usr/lib/yp/ypbind` 命令），并在主服务器宕机时向客户端提供这些映射。

你可以将 NIS 理解为一种在 NIS 域内的所有客户端之间分发相同配置文件的方法。你可以共享相同文件的优势（例如所有机器使用相同的用户名和密码），只需编辑和维护主 NIS 服务器上的文件。

在接下来的章节中，我将解释如何将你的 Red Hat Linux 系统配置为 NIS 客户端和 NIS 服务器。

# 设置 NIS 客户端

如果你需要通过 NIS 集中管理用户和密码，可以将你的 Red Hat Linux PC 设置为 NIS 客户端。事实上，当你从本书的附带光盘中中安装 Red Hat Linux 时，可以在 GUI 安装程序的“身份验证配置”（Authentication Configuration）屏幕中启用 NIS。

在 Red Hat 安装过程中，身份验证配置屏幕向你展示了多种验证用户的选项——默认是影子密码（shadow passwords）和 MD5 密码。这些选项之一是一个标记为“启用 NIS”的按钮。你可以点击它来将你的 Red Hat Linux PC 设置为 NIS 客户端。当然，只有当你的网络已设置了 NIS 服务器时才应该这样做。

第八卷

第 5 章

DNS 与 NIS

设置

# 690 理解网络信息服务 (NIS)

如果你决定启用“启用 NIS”选项，你必须提供以下信息：

- 指定 NIS 域名。域名指的是 NIS 服务器所服务的计算机组。
- 指定 NIS 服务器的名称。
- 指定你是否希望你的 PC 使用 IP 广播来查找局域网内的 NIS 服务器。

如果你在 Red Hat Linux 安装期间没有将系统配置为 NIS 客户端，可以通过执行以下通用步骤来完成：

1. 定义你的 NIS 域名。
2. 设置你的 NIS 配置文件（`/etc/yp.conf`）。
在此文件中，你指定了为你的 Red Hat Linux PC 提供 NIS 映射的主 NIS 和从服务器。
3. 配置 NIS 客户端守护进程——`ybind`——在系统启动时启动。

我将在接下来的章节中向你展示如何执行完成这些任务的特定步骤。

# NIS 域名设置

域名标识了特定 NIS 服务器支持的计算机组。你可以使用 `domainname` 命令设置系统的 NIS 域。例如，要将域名设置为 `admin`，请登录 root 并在终端中输入以下内容：

```
domainname admin
```

如果你输入没有任何参数的 `domainname`，该命令将打印当前的 NIS 域名。为了确保 NIS 域名在系统启动时被设置，应该从其中一个启动脚本运行该命令。你可以通过向 `/etc/network` 添加以下行来实现：

```
NISDOMAIN="admin"
```
