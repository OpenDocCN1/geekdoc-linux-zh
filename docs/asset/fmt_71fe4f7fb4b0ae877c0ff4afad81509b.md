
| knetd | 2053/tcp | | Kerberos 解复用器 |

| zephyr-srv | 2102/udp | | Zephyr 服务器 |

| 服务 | 端口/协议 | 别名 | 注释 |

| :--- | :--- | :--- | :--- |

| zephyr-clt | 2103/udp | | Zephyr serv-hm 连接 |

| zephyr-hm | 2104/udp | | Zephyr 主机管理器 |

| eklogin | 2105/tcp | | Kerberos 加密登录 |

### 非官方但必要（针对 NetBSD）的服务

| 服务 | 端口/协议 | 别名 | 注释 |

| :--- | :--- | :--- | :--- |

| supfilesrv | 871/tcp | | SUP 服务器 |

| supfiledbg | 1127/tcp | | SUP 调试 |

### 数据报交付协议服务

| 服务 | 端口/协议 | 别名 | 注释 |

| :--- | :--- | :--- | :--- |

| rtmp | 1/ddp | | 路由表维护协议 |

| nbp | 2/ddp | | 名称绑定协议 |

| echo | 4/ddp | | AppleTalk 回显协议 |

| zip | 6/ddp | | 区域信息协议 |

### Debian GNU/Linux 服务

| 服务 | 端口/协议 | 别名 | 注释 |

| :--- | :--- | :--- | :--- |

| rmtcfg | 1236/tcp | | Gracilis Packeten 远程配置服务器 |

| xtel | 1313/tcp | | 法国 minitel |

| cfinger | 2003/tcp | | GNU Finger |

| postgres | 4321/tcp | | POSTGRES |

| mandelspawn | 9359/udp | | 网络分形（曼德博） |

### 本地服务

在现实世界中，随着新服务的创建，实际文件始终在不断增长。如果您担心自己的副本不完整，我建议从最新的发行版中复制一份新的 `/etc/services`。

### `/etc/inetd.conf`

`/etc/inetd.conf` 文件是 `inetd` 服务器守护进程的配置文件。其功能是告诉 `inetd` 在收到特定服务的连接请求时该做什么。对于您希望接受连接的每个服务，您必须告诉 `inetd` 要运行哪个网络服务器守护进程以及如何运行它。

其格式也相当简单。它是一个文本文件，每一行描述您希望提供的服务。行中“`#`”之后的任何文本都会被忽略并视为注释。每一行包含由任意数量的空白字符（制表符或空格）分隔的七个字段。通用格式如下：

```
service socket_type proto flags user server_path server_args
```

`service` 是指与此配置相关的服务，取自 `/etc/services` 文件。

`socket_type` 此字段描述此条目将视为相关的套接字类型；允许的值为：`stream`、`dgram`、`raw`、`rdm` 或 `seqpacket`。这在技术上有点复杂，但作为一个经验法则，几乎所有基于 `tcp` 的服务都使用 `stream`，几乎所有基于 `udp` 的服务都使用 `dgram`。只有非常特殊的类型服务器守护进程才会使用其他任何值。

`proto` 被视为对此条目有效的协议。这应与 `/etc/services` 文件中的相应条目匹配，通常要么是 `tcp` 要么是 `udp`。基于 Sun RPC（远程过程调用）的服务器将使用 `rpc/tcp` 或 `rpc/udp`。

`flags` 此字段实际上只有两种可能的设置。此字段设置告诉 `inetd` 网络服务器程序在启动后是否释放套接字，从而决定 `inetd` 是否可以在下一个连接请求时启动另一个，或者 `inetd` 是否应该等待并假设已经在运行的任何服务器守护进程都会处理新的连接请求。再次说明，这有点棘手，但作为一个经验法则，所有 `tcp` 服务器都应将此条目设置为 `nowait`，大多数 `udp` 服务器应将此条目设置为 `wait`。我警告过存在一些显著的例外，因此如果您不确定，请让示例引导您。

`user` 此字段描述启动时哪个 `/etc/passwd` 中的用户账户将被设置为网络守护进程的所有者。如果您希望防范安全风险，这通常很有用。您可以将条目的用户设置为 `nobody` 用户，以便如果网络服务器安全被突破，可能的损害会最小化。不过，此字段通常设置为 `root`，因为许多服务器需要 root 权限才能正确运行。

`server_path` 此字段是为该条目要执行的实际服务器程序的路径名。

`server_args` 此字段组成行的其余部分，并且是可选的。此字段是您在启动服务器守护进程程序时想要传递任何命令行参数的位置。

#### `/etc/inetd.conf` 示例

与 `/etc/services` 文件类似，所有现代发行版都会提供一个可用的良好 `/etc/inetd.conf` 文件供你使用。为了完整性，以下是 Debian 发行版（参见 `http://www.debian.org/`）的 `/etc/inetd.conf` 文件：
