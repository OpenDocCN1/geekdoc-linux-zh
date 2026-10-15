
```
root# chown maryo a_file
chown: 'maryo': invalid user
```

“这快让我疯了！可能是什么问题？”

你的系统很可能正在运行 `nscd`（名称服务缓存守护进程）。请将其关闭，不要重启它！你会发现问题已解决。

# 28. 将 MS Windows 网络与 Samba 集成

本章讨论 NetBIOS over TCP/IP 的名称到 IP 地址解析。如果你的 MS Windows 客户端未配置为使用 NetBIOS over TCP/IP，则本节不适用于你的安装。如果你的安装涉及使用 NetBIOS over TCP/IP，那么本章可能有助于你解决网络问题。

> **注意**
>
> NetBIOS over TCP/IP 与 NetBEUI 没有任何关系。NetBEUI 是 NetBIOS over 逻辑链路控制 `LLC`。在现代网络中，强烈建议完全不要运行 NetBEUI。还要注意，不存在所谓的“NetBEUI over TCP/IP”——认为存在这样的协议是一个完全错误的误解。

## 28.1 特性与优势

许多 MS Windows 网络管理员从未接触过在 UNIX/Linux 操作系统中实现的基本 TCP/IP 网络。同样，许多 UNIX 和 Linux 管理员也没有接触过基于 MS Windows TCP/IP 网络的复杂性（并且可能也不希望接触）。

本章简要介绍了如何在每种操作系统环境中将名称解析为其 IP 地址的基础知识。

## 28.2 背景信息

自 MS Windows 2000 推出以来，可以在不使用 NetBIOS over TCP/IP 的情况下运行 MS Windows 网络。NetBIOS over TCP/IP 使用 UDP 端口 `137` 进行 NetBIOS 名称解析，并使用 TCP 端口 `139` 进行 NetBIOS 会话服务。当在 MS Windows 2000 及更高版本的客户端上禁用 NetBIOS over TCP/IP 时，则仅使用 TCP 端口 `445`，而不使用 UDP 端口 `137` 和 TCP 端口 `139`。

> **注意**
>
> 当使用 Windows 2000 或更高版本的客户端时，如果没有禁用 NetBIOS over TCP/IP，客户端将使用 UDP 端口 `137`（NetBIOS 名称服务，也称为 Windows Internet 名称服务或 WINS）、TCP 端口 `139` 以及 TCP 端口 `445`（用于实际的文件和打印流量）。

当禁用 NetBIOS over TCP/IP 时，必须使用 DNS。当今大多数禁用 NetBIOS over TCP/IP 的安装使用 MS Active Directory 服务 `ADS`。`ADS` 需要动态 DNS 服务资源记录 `SRV RR` 和增量区域传输 `IXFR`。建议结合使用 DHCP 和 ADS，作为对客户端工作站网络配置进行集中控制的进一步手段。

## 28.3 纯 UNIX/Linux 环境中的名称解析

本节涉及的关键配置文件包括：

- `/etc/hosts`
- `/etc/resolv.conf`
- `/etc/host.conf`
- `/etc/nsswitch.conf`

### 28.3.1 `/etc/hosts`

此文件包含 IP 地址和名称的静态列表。

```
127.0.0.1 localhost localhost.localdomain
192.168.1.1 bigbox.quenya.org bigbox alias4box
```

`/etc/hosts` 的目的是提供一种名称解析机制，以便用户无需记忆 IP 地址。

通过物理网络传输层发送的网络数据包并不是通过 IP 地址通信，而是使用媒体访问控制地址（MAC 地址）。IP 地址目前长度为 32 位，通常表示为由点（或句点）分隔的四个十进制数——例如 `168.192.1.1`。

MAC 地址使用 48 位（或 6 字节），通常表示为以冒号分隔的双位十六进制数：`40:8e:0a:12:34:56`。

每个网络接口都必须有一个 MAC 地址。与 MAC 地址相关联的可以是一个或多个 IP 地址。IP 地址和 MAC 地址之间没有关联关系；所有这些分配在本质上是任意的或酌情决定的。在最基本的层面上，所有网络通信都使用 MAC 寻址进行。由于 MAC 地址必须全球唯一，并且通常对于任何特定接口都保持固定，因此从网络管理角度来看，分配 IP 地址是有意义的。每个 MAC 地址可以分配多个 IP 地址。其中一个地址必须是主 IP 地址；这是在地址解析协议 `ARP` 响应中返回的地址。

当用户或进程想要与另一台机器通信时，协议实现会确保以 TCP/IP 配置文件控制的方式将“机器名称”或“主机名”解析为 IP 地址。文件 `/etc/hosts` 就是其中一个这样的文件。

当确定目标接口的 IP 地址后，使用称为 `ARP/RARP` 的协议来识别目标接口的 MAC 地址。`ARP` 是一种面向广播的方法，它使用用户数据报协议 `UDP` 向本地网段上的所有接口发送请求，使用的是全 1 的 MAC 地址。网络接口被编程为仅响应两个 MAC 地址：其自身唯一的地址和地址 `ff:ff:ff:ff:ff:ff`。来自 `ARP` 请求的响应包将包含每个接口的 MAC 地址和主 IP 地址。

`/etc/hosts` 文件是所有 UNIX/Linux TCP/IP 安装的基础，至少包含 `localhost` 和本地网络接口的 IP 地址以及它们在本地机器内已知的原始名称。此文件有助于启动解析过程，使得在任何其他名称解析方法可用之前，都能存在基本级别的名称解析。

### 28.3.2 `/etc/resolv.conf`

此文件告诉名称解析库：

- 机器所属的域名。
- 在尝试将未限定主机名解析为其 IP 地址时应自动搜索的任何域名。
- 可用于执行名称到地址转换查询的域名服务器的名称或 IP 地址。

### 28.3.3 `/etc/host.conf`

`/etc/host.conf` 是让 `/etc/resolv.conf` 中的设置生效的主要方式。它是一个关键的配置文件。此文件控制名称解析进行的顺序。典型结构如下：

```
order hosts,bind
multi on
```

所有地址都应返回。有关更多详细信息，请参阅 `host.conf` 的 man 页面。

### 28.3.4 `/etc/nsswitch.conf`

此文件控制实际的名称解析目标。该文件通常具有如下所示的解析器对象规范：

```
# /etc/nsswitch.conf
#
# Name Service Switch configuration file.
#

passwd:    compat
# Alternative entries for password authentication are:
# passwd:  compat files nis ldap winbind
shadow:    compat
group:     compat

hosts:     files nis dns
# Alternative entries for host name resolution are:
# hosts: files dns nis nis+ hesiod db compat ldap wins
networks:  nis files dns

ethers:    nis files
protocols: nis files
rpc:       nis files
services:  nis files
```

当然，这些机制中的每一个都需要正确配置相应的设施和/或服务。

需要注意的是，除非必须发送网络请求/消息，TCP/IP 网络是静默的。所有 TCP/IP 通信都遵循仅在必要时才发声的原则。

从版本 `2.2.0` 开始，Samba 支持对名称服务切换（NSS）基础设施的扩展，以便 Linux 客户端能够解析 MS Windows NetBIOS 名称至 IP 地址。要获得此功能，Samba 需要在 `make` 命令中传入相应的参数进行编译（即 `make nsswitch/libnss_wins.so`）。生成的库文件应安装到 `/lib` 目录中，并且需要在 `/etc/nsswitch.conf` 文件的 `hosts:` 行中添加 `wins` 参数。此时，只要 Samba 机器和 MS Windows 机器属于同一工作组，就可以通过 NetBIOS 机器名 ping 任何 MS Windows 机器。

## 28.4 MS Windows 网络中使用的名称解析
