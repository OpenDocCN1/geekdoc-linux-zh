
# 习题

- 1. 以下哪个 `Squid` 设置允许你使用 `LDAP` 服务器对客户端进行身份验证？
  a. `auth_client`
  b. `auth_ldap`
  c. `auth_server`
  d. `auth_param`

- 2. `Squid` 的 `___` 设置允许你将机器名称组合并在一个别名下。

- 3. `Squid` 的 `___` 设置允许你指定哪些机器可以使用 `Squid` 服务器。

- 4. `___` 软件既可以作为代理服务器使用，也可以作为 Web 服务器使用。

- 5. 一旦你正确配置了 `Squid` 代理服务器，你还应该配置一个 `___` 来测试该代理服务器。
  a. Web 服务器
  b. 路由器
  c. Web 浏览器
  d. `LDAP` 服务器

# 基础服务器主题

代理服务器是一种促进客户端与服务器之间通信的系统。根据代理服务器的设计，有几种不同的代理服务器以及不同的优势。表 25-2 描述了代理服务器的类型以及每种类型/优势。

## 表 25-2 代理服务器

| 代理服务器类型 | 描述和优势 |
|--- | --- |
| 隧道代理 (Tunneling proxy) | 这种代理旨在作为两个网络之间的网关。例如，当基于 `IPv4` 的网络需要与基于 `IPv6` 的网络通信时。请参图 25-1 查看隧道代理的视觉示例。隧道代理不包含在 `LPIC-2` 考试目标中。 |
| 正向代理 (Forward proxy) | 这种代理旨在工作在通信的客户端侧。例如，Web 浏览器可以指向代理服务器，而不是直接与 Web 服务器通信。通常，当有人调用系统代理服务器时，她指的是一个作为正向代理的系统。请参图 25-2 查看正向代理的视觉示例。 |

正向代理服务器可以提供几个关键功能，包括：

- 它可以通过阻塞对外部资源的访问来充当过滤器。
- 它可以充当客户端和服务器之间的缓冲区，因为服务器“看到”请求来自代理服务器，而不是原始客户端。这可以隐藏原始客户端数据，例如其 `IP` 地址或位置。某些用户更倾向于此，因为它允许匿名浏览。这对于绕过限制也非常有用；例如，只允许从特定地理区域访问的网站。在这种情况下，位于正确地理区域的代理服务器可以允许所需的访问。
- 代理服务器可以缓存静态数据；例如，具有静态 Web 页面的网站。当多个代理客户端尝试检索相同数据时，代理服务器可以通过直接返回数据来加速过程，而不是反复查询 Web 服务器。

# 代理服务器描述和优势

代理服务器可以记录客户端活动。

图 25-2 正向代理

反向代理服务器（Reverse proxy server）是配置在服务器端的。例如，与其让 Web 客户端直接连接到你公司的 Web 服务器，不如让他们先连接到代理服务器。代理服务器与 Web 服务器通信获取所需数据。请参图 25-3 查看反向代理的视觉示例。

反向代理服务器有几个优势，包括：

- 代理服务器可以提供负载均衡，因为它可以向多个 Web 服务器发送查询。
- 反向代理可以通过缓存静态数据来限制反向服务器的负载。
- 对于基于 `SSL` 的 Web 服务器，代理服务器可以执行 `SSL` 操作，而不是 Web 服务器。如果代理服务器配备了 `SSL` 加速硬件，这将是一个巨大的优势。
- 代理服务器可以有效地从客户端隐藏 Web 服务器，使 Web 服务器更安全。由于无法直接访问 Web 服务器，利用该服务器将变得困难。
- 代理服务器可以通过压缩数据来优化通信，提高数据传输速度。

并不是所有的代理优势都是可测试的，但了解它们可以让你在考虑部署反向代理服务器时做出更好的决策。

图 25-3 反向代理

许多软件项目提供代理服务器。两种最常见的代理服务器是 `LPIC-2` 考试测试：

- `Nginx`（读作 "engine x"）——`Nginx` 可以作为多种协议（包括 `HTTP` 和 `HTTPS`）的反向代理服务器。通常，它用于为 Web 服务器提供负载均衡和缓存功能。它也可以单独被配置为 Web 服务器。
- `Squid`——该软件既用作正向又是反向代理服务器。它源于科罗拉多大学博尔德分校开发的 `Harvest` 对象缓存项目。它从该原始项目分支并命名为 `Squid`。一个商业版本（`NetCache`，现已停止开发）也从该项目分支而出。本章重点介绍如何将 `Squid` 配置为代理服务器。

# Squid 基础

注意：`LPIC-2` 考试题的重点是将 `Squid` 配置为正向代理服务器。

虽然在发行版中默认安装 `Apache` Web 服务器非常常见，但安装 `Squid` 并不常见。因此，你的首要任务是使用管理系统（`yum` 或 `apt-get`）安装 `Squid`。安装过程应包含一个基础配置文件，通常位于 `/etc/squid/`。

## 表 25-3 代理设置

| Squid 设置 | 描述 |
|--- | --- |
| `cache_dir` | 当 `Squid` 作为正向代理工作时，它应该缓存静态数据。要设置此项，请使用以下：``cache_dir ufs /var/spool/squid 100 16 256``。值 `ufs` 表示存储类型。值 `/var/spool/squid` 是缓存位置。值 `100` 是缓存文件（总计）的最大大小，单位为 `MB`。值 `16` 和 `256` 指将创建的一级和二级子目录的数量。 |

# Squid 设置描述

`http_port` 这是 `Squid` 服务器监听传入请求的端口号。通常将其设置为 `3128`，但也经常将其设置为 `8080`。示例：

```
http_port 3128
```

`auth_param` 此选项允许使用各种身份验证方法对客户端进行验证。例如，你可以使用 `LDAP` 或 `Samba` 服务器进行验证。

在大多数情况下，我们通过指定允许哪些客户端系统来限制对 `Squid` 服务器的访问。

`acl` 此选项提供了一种将源和目标网络、地址、端口和其他安全设置组合并为该组分配名称的能力。这在你想要允许或拒绝访问 `Squid` 服务器时有用。`acl` 选项将在下一节中详细介绍。

`http_access` 此选项用于指定哪个 `acl` 名称允许使用 `Squid` 服务器作为 `HTTP` 代理服务器。`http_access` 选项将在下一节中详细介绍。

> **注意：** 术语 `acl` 代表访问控制列表（access control list）。

# Squid 访问规则

在大多数情况下，你希望限制仅特定系统访问你公司的 `Squid` 服务器。这是通过首先使用 `acl` 语句创建机器组，然后使用 `http_access` 语句允许（或拒绝）访问来实现的。

## 第2章：实现代理服务器

```config
acl localnet src 192.168.0.0/16 # RFC1918 可能的内部网络
acl localnet src fc00::/7 # RFC 4193 本地私有网络范围
acl localnet src fe80::10 # RFC 4291 链路本地（直接插入）机器
acl Safe_ports port 443
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 # https
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # wais
acl Safe_ports port 1025-65535 # 未注册
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filemaker
acl Safe_ports port 777 # 多主机托管 http
acl CONNECT METHOD Safe_ports
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost manager
http_access deny manager
http_access allow localnet
http_access deny all
http_port 3128
coredump_dir /var/spool/squid
refresh_pattern "ftp": 1440 20% 10080
refresh_pattern "gopher": 1440 0% 1440
refresh_pattern -i (cgi-bin/\?) 0 0% 0
refresh_pattern - 0 20% 4320
```

`acl` 语句的基本语法为：

`acl name type data`

`name` 是你自定义的。例如，在以下条目，`localnet` 并不是某个特殊的定义名称，而只是一个根据其描述的内容（本地网络）命的名字：
