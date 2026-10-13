
# wu-ftp 配置文件基本示例（继续）

|  |  |  |  |  |  |
|---|---|---|---|---|---|
| upload `/var/ftp` `/etc` | no daemon 0600 dirs |
| upload `/var/ftp` `/incoming` | yes root |

* 目录别名。[注意，不需要冒号 “:”]

`aliases inc: /incoming`

* `cdpath`

`cdpath /incoming`

`cdpath /pub`

`cdpath /`

* `path-filter`...路径过滤器……

`path-filter anonymous /etc/pathmsg "-[A-Za-z0-9_].*s" -,`

`path-filter guest /etc/pathmsg "-[A-Za-z0-9_].*s" -`

* 指定哪些组的用户被视为“客人”

`guestgroup ftpponly`

```
email user@hostname # 应该更改真实的电子邮件地址
[root]@linux:/root]*
==================================================
```

![](img/d93cde4788f2827fc3c67c2526fc3dc0_457_0.png)

你需要安装 `anftpd` 包来提供匿名 FTP 服务。只有当你想要为各种组和用户登录访问添加安全设置时，才需要 `wu-ftpd`。

## 认证目标 8.03

# Samba

从 Windows 3.11 开始，Windows 客户端可以“共享它们的文件系统和打印机，供其他 Windows 客户端将其“映射”为远程资源。这种共享通过名为 SMB（Server Message Block，又称 NetBIOS）的功能提供。通过 Andrew Tridell 等许多人的共同努力，Linux 系统通过名为 Samba 的包在 TCP/IP 上提供了 SMB 支持。

## Samba 417

使用 Samba 可以完成四件基本的“事情”：

- 与 Windows 机器共享 Linux 目录树
- 与 Linux 机器共享 Windows 磁盘
- 与 Windows 机器共享 Linux 打印机
- 与 Linux 机器共享 Windows 打印机

Samba 通过 SMB 协议实现了许多与 Win9x 和 NT 操作系统相关的高级网络特性和功能。完整信息可以在 http://nimbus.anu.edu.au/pub/bridge/samba/ 找到。

Samba 可以轻松配置为：

- 共享用户主目录服务
- 成为任何 WINS 服务的服务器或客户端
- 连接或管理工作组浏览服务
- 如果存在多个工作组，则成为主浏览器服务
- 通过本地登录安全或 NT PDC 权威对所有共享访问请求进行身份验证
- 作为挂载的 SMB 文件服务提供本地目录连接
- 提供域登录验证服务
- 在 Windows 和 Linux 系统之间同步密码

虽然有很多方面，但你大概明白意思了。这些都源自一个长文件。当你第一次看到这个文件时，可能会被这些细节所淹没。下一节将把这个文件拆解成更易理解的部分。

## 安装 Samba

如果你进行的是服务器安装（Server installation），则 Samba 包已经安装了。如果你进行的是工作站安装（Workstation installation），则默认没有安装 Samba。如果你

### # 418 第 8 章：网络客户端服务

进行了自定义安装（Custom installation），你可能选择了了 Samba 服务。你可以通过 RPM 查询所有已安装的包，然后 `grep Samba` 来查看是否存在。

## 第 8 章：网络客户端服务

Samba 的安装见图 8-1。

## Samba 服务的基础

Samba 服务的实现了许多与 Win9x 和 NT 操作系统相关的高级网络特性和功能，通过 SMB 协议。完整信息可以在 http://nimbus.anu.edu.au/pub/bridge/samba/ 找到。

Samba 可以轻松配置为：

- 共享用户主目录服务
- 成为任何 WINS 服务的服务器或客户端
- 连接或管理工作组浏览服务
- 如果存在多个工作组，则成为主浏览器服务
- 通过本地登录安全或 NT PDC 权威对所有共享访问请求进行身份验证
- 作为挂载的 SMB 文件服务提供本地目录连接
- 提供域登录验证服务
- 在 Windows 和 Linux 系统之间同步密码

虽然有很多方面，但你大概明白意思了。这些都源自一个长文件。当你第一次看到这个文件时，可能会被这些细节所淹没。下一节将把这个文件拆解成更易理解的部分。

## 图 8-17

Samba 的安装

```
==================================================
[root]@linux6 #] rpm -qa
(未找到则无输出)
[root]@linux6 #] mount /mnt/cdrom
[root]@linux6 #] cd /mnt/cdrom/Redhat/RPMS/
[root]@linux6 #] rpm -iv samba-2.0.3.1386
samba-2.0.3-8
[root]@linux6 #] rpm -qa
samba-2.0.3-8
[root]@linux6 #] umount /mnt/cdrom
==================================================
```

实现了许多与 Win9x 和 NT 操作系统相关的高级网络特性和功能，通过 SMB 协议。完整信息可以在 http://nimbus.anu.edu.au/pub/bridge/samba/ 找到。

Samba 可以轻松配置为：

- 共享用户主目录服务
- 成为任何 WINS 服务的服务器或客户端
- 连接或管理工作组浏览服务
- 如果存在多个工作组，则成为主浏览器服务
- 通过本地登录安全或 NT PDC 权威对所有共享访问请求进行身份验证
- 作为挂载的 SMB 文件服务提供本地目录连接
- 提供域登录验证服务
- 在 Windows 和 Linux 系统之间同步密码

# 域名解析——DNS

互联网演化出一种分布式服务来提供主机到 IP 的解析，称为域名服务（DNS）。DNS 设计将数据库分布在任意数量的服务器上，运行带有静态（文本文件）的本地 DNS 服务。DNS 记录简单来说主机名和相关的 IP 地址。

| DNS 名称 | 类型 | IP 地址 |
|---|---|---|
| www.foo.bar | A | 10.1.1.1 |
| ftp.foo.bar | A | 10.1.1.2 |

（2 DNS 地址记录）

你输入 `www.foo.bar`，DNS 返回 IP 地址 `10.1.1.1`；无论从哪个 DNS 服务器获取代表的名称记录。

每个 DNS 服务器仅维护本地局域网主机列表。DNS 在大多数情况下是手动管理的；每条记录都添加到配置文件中。

Windows 的大师们决定创建他们自己的集中式服务，由主机在启动时动态更新。这种仅基于动态的服务被称为 Windows 内部命名服务（WINS）。WINS 是 IP 地址和相关 NetBIOS 名称的数据库。互联网不使用 WINS；它只使用 DNS。

对于几乎所有的网络客户端，有一种自动 IP 配置服务，称为动态主机配置协议（DHCP）。当 DHCP

## 420 第 8 章：网络客户端服务

客户端启动时，会向网络服务发送 IP 配置信息的请求。DHCP 服务器可以为客户端提供所有的网络信息，加上额外的 Windows IP 参数信息，如果客户端是基于 Windows 的系统，特别是 WINS IP 地址。

## 域名解析—WINS

WINS 被设计为一种动态（客户端在启动时添加记录）、集中化（所有记录都存储在一个或多个中央服务器上）且健壮的服务，它是 DNS 的替代方案，如果配置得当，它可以提供对基于 Windows 的客户端局域网的 WAN“浏览”。

每个 WINS 服务器都维护一个包含所有机器多个记录的中央数据库。在大型网络中，这是一个大数据文件。对于每个主机，可以向 WINS 添加至少 3 条到最多 10 条或更多记录，以满足所有的 Windows 网络需求。自然，随着网络规模的扩大，这种每个格式多个记录变得非常繁琐。在接下来的几个版本中，WINS 将被淘汰。

UNIX 系统也有自己的用于用户和网络访问的认证服务。Windows 拥有 NT 域（Domain）或 LAN Manager 认证系统设计。它们基于不同的策略设计，互操作性最初并不是它们的考虑因素。

## SAMBA 又是怎样的？
