
408 TCP/IP 基础

```bash
(Linux):~# rpcinfo -p
program vers proto port
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
100005 1 udp 668 mountd
100005 1 tcp 670 mountd
100003 2 udp 2049 nfs
100003 2 tcp 2049 nfs
100004 2 udp 698 ypserv
100004 1 udp 698 ypserv
100004 2 tcp 701 ypserv
100007 2 udp 709 ybindd
100007 2 tcp 711 ybindd
```

**列表 14.8** 计算机的 RPC 服务

```bash
(Linux):~# rpcinfo -u localhost 100004 2
program 100004 version 2 ready and waiting
(Linux):~# rpcinfo -u localhost 100004
program 100004 version 1 ready and waiting
program 100004 version 2 ready and waiting
```

**列表 14.9** rpcinfo 程序

如果你正在寻找在局域网中提供特殊服务的计算机，必须使用 `-b` 选项。这将创建一个广播，由提供该服务的服务器进行响应。可以在列表 14.10 中找到示例。

```bash
(Linux):~# rpcinfo -b localhost 100004 2
127.0.0.1 localhost
192.168.3.155 26 pea.example.org
127.0.0.1 localhost
192.168.3.155 26 pea.example.org
127.0.0.1 localhost
192.168.3.155 26 pea.example.org
```

**列表 14.10** rpcinfo 程序

## 14.7 与体系无关的数据格式

网络通信对几乎任何计算机架构都是开放的。这为协议和程序的开发带来了许多问题。其中一个问题是不同字符集（ASCII、ISO Latin-1 或 EBCDIC）中文本的编码方式不同。

另一个问题是整数的内部表示方式不同。在传输之前（例如作为端口号），必须将其转换为网络字节序。这是通过 C 语言函数 `htons(3)` 实现的。如果当前架构的内部数据格式与网络字节序相等，则不进行转换。图 14.1 显示了不同计算机架构上 IP 地址的不同表示示例。

网络字节序（例如 68000 CPU）：

| 192 | 168 | 31 | 155 |
| :--- | :--- | :--- | :--- |

Intel 80x86 CPU：

| 155 | 31 | 168 | 192 |
| :--- | :--- | :--- | :--- |

**图 14.1** IP 地址 192.168.3.155 的内部表示。

对于其他数据的交换，文本可能需要重新编码或转换数据库文件。为了这些目的，开发了一系列工具，如用于文本文件的 `recode` 或特殊库。关于“外部数据表示”（External Data Representation）的更多细节可以在 [rfc1014] 中找到。

## IP 地址和计算机名称 15

到目前，我们几乎只使用数值 IP 地址。这些地址在相关系统内部使用，但对于人类用户来说，它们比名称更记忆。因此，除了数值 IP 地址外，每台计算机还分配了一个名称，可以通过该名称进行寻址。这需要在名称和 IP 地址之间进行自动的双向转换。

UNIX 系统的主机名在系统启动时通过 `hostname` 命令设置。互联网上有成千上万台计算机，它们必须具有唯一的地址。因此，IP 地址和主机名必须是唯一的。

如果仅使用单词作为名称（如在 UUCP 地图中很常见），将很难找到唯一的名称。解决方案是使用域名。域名例如是指一个公司或大学的组织同质化网络。在 LINUX 下，通过 `dnsname` 设置域名。

命名空间由许多顶级域名（如 ...）划分。

- 如果仅使用单词作为名称（如在 UUCP 地图中很常见），将很难找到唯一的名称。解决方案是使用域名。
- 域名例如是指一个公司或大学的组织同质化网络。
- 域名在 LINUX 下通过 `dnsname` 设置。

命名空间由许多顶级域名（如 ...）划分。

