

## 9.4.7 远程通告参数的使用

你正在处理的机器拥有 4 个网络接口：eth0、eth1、eth2 和 eth3，并且只有 eth1 和 eth4 接口应被 Samba 使用。在这种情况下，以下 `smb.conf` 文件条目将允许实现该意图：

```
interfaces = eth1, eth4
bind interfaces only = Yes
```

`bind interfaces only = Yes` 是必要的，以排除未指定接口上的 TCP/IP 会话服务（端口 135、139 和 445）。请注意，`nmbd` 将在未列出的接口上监听传入的 UDP 端口 137 数据包，但不会响应它们。然而，它会通过未列出的接口发送广播数据包。要完全隔离以太网接口，需要使用防火墙来阻止所有必须无法访问 Samba 服务器的网络接口上的端口 137 和 138（UDP），以及端口 135、139 和 445（TCP）。

`smb.conf` 中的 `remote announce` 参数可用于强制确保网络上的所有 NetBIOS 名称都被通告到远程网络。`remote announce` 参数的语法如下：

```
remote announce = 192.168.12.23 [172.16.21.255] ...
```

或者

```
remote announce = 192.168.12.23/MIDEARKH [172.16.21.255/ELVINDORF] ...
```

其中：

-   192.168.12.23 和 172.16.21.255 是远程网络的 LMB IP 地址或广播地址。也就是说，LMB 位于 192.168.1.23，或者地址可以表示为 172.16.21.255，假设子网掩码为 24 位（255.255.255.0）。当向远程网络的广播地址进行远程通告时，每台主机都会收到我们的通告。这会产生大量流量，因此通常不受欢迎，但如果我们不知道远程 LMB 的 IP 地址，则可能是必要的。
-   WORKGROUP 是可选的，可以是自己的工作组或远程网络的工作组。如果使用远程网络的工作组名称，我们的 NetBIOS 机器名称将看起来属于该工作组。这可能会导致名称解析问题，应避免。

## 9.4.8 远程浏览同步参数的使用

`smb.conf` 中的 `remote browse sync` 参数用于向另一个 LMB 通告，它必须将其 NetBIOS 名称列表与我们的 Samba LMB 同步。这仅当拥有此选项的 Samba 服务器同时是其网络段上的 LMB 时有效。

*remote browse sync* 参数的语法是：

```
remote browse sync
```

其中 *192.168.10.40* 是远程 LMB 的 IP 地址或远程网段的网络广播地址。

### 9.5 WINS：Windows 互连网络名称服务器

强烈建议使用 WINS（无论是 Samba WINS 还是 MS Windows NT Server WINS）。每台 NetBIOS 机器都会针对其提供的几种服务类型，连同其 *name_type* 值一起注册其名称。它直接将其名称注册为一个唯一名称（类型为 *0x03*）。如果它运行 LanManager 兼容服务器服务（用于使共享和打印机可供其他用户访问），它也通过注册服务器名称（类型为 *0x20*）来注册其名称。

所有 NetBIOS 名称的长度最多为 15 个字符。*name_type* 变量被添加到名称的末尾，从而创建一个 16 字符的名称。任何短于 15 个字符的名称都会用空格填充至第 15 个字符。因此，所有 NetBIOS 名称均为 16 个字符长（包括 *name_type* 信息）。

WINS 可以在这些 16 字符的名称被注册时存储它们。想要登录网络的客户端可以向 WINS 服务器请求所有已注册 NetLogon 服务 *name_type* 的名称列表。这节省了广播流量，并极大地加快了登录处理。由于广播名称解析无法跨网络段使用，因此这类信息只能通过 *WINS* 提供，或者在没有 WINS 的情况下，通过必须位于所有客户端上的静态配置的 *lmhosts* 文件提供。

WINS 还强制所有 LMB 进行浏览列表同步。LMB 必须与其 DMB 同步浏览列表，WINS 有助于 LMB 识别其 DMB。根据定义，这仅在单个工作组内有效。请注意，DMB 与所谓的 MS Windows NT 域无关。后者指的是安全环境，而 DMB 仅指浏览列表信息的掌握控制器。

WINS 仅在配置为使用 WINS 服务器的每个客户端 TCP/IP 协议栈都正确配置时才能正常工作。任何未配置为使用 WINS 服务器的客户端将继续仅使用基于广播的名称注册，因此 WINS 可能永远无法得知该客户端的存在。无论如何，未向 WINS 服务器注册的机器将无法通过其他客户端进行的名称到地址的查找，因此会导致工作站访问错误。

要将 Samba 配置为 WINS 服务器，只需在 **smb.conf** 文件的 [global] 部分中添加 `wins support = yes`。

要将 Samba 配置为向 WINS 服务器注册，只需在你的 **smb.conf** 文件 [global] 部分中添加 `wins server = 10.0.0.18`。

> **重要**
> 切勿将 `wins support = yes` 与 `wins server = 10.0.0.18` 一起使用，特别是不要使用其自身的 IP 地址。同时指定这两项将导致 `nmbd` 拒绝启动！

### 9.5.1 WINS 服务器配置

Samba 服务器或 Windows NT 服务器机器都可以设置为 WINS 服务器。要将 Samba 服务器配置为 WINS 服务器，必须在选定的服务器的 `smb.conf` 文件的 [global] 部分中添加以下行：

```
wins support = yes
```

1.9.17 之前的 Samba 版本将此参数的默认值设为 yes。如果你的网络上有较旧版本的 Samba，强烈建议你升级到最新版本，或者至少在所有这些机器上将该参数设置为 "no"。

配置为 `wins support = yes` 的机器将保持所有已注册 NetBIOS 名称的列表，充当 NetBIOS 名称的 DNS。

强烈建议只设置一个 WINS 服务器。不要在一个网络上的多台 Samba 服务器上设置 `wins support = yes` 选项。

要将 Windows NT/200x Server 配置为 WINS 服务器，请安装并配置 WINS 服务。有关详细信息，请参阅 Windows NT/200x 文档。Windows NT/200x WINS 服务器可以相互复制，允许在复杂的子网环境中设置多个 WINS 服务器。由于 Microsoft 拒绝记录复制协议，Samba 无法正确参与这些复制。未来可能会定义 Samba 到 Samba 的 WINS 复制协议，在这种情况下，可以设置多台 Samba 机器作为 WINS 服务器。目前，应该只有一台 Samba 服务器设置 `wins support = yes` 参数。

配置 WINS 服务器后，必须确保参与网络的所有机器都配置了该 WINS 服务器的地址。如果你的 WINS 服务器是一台 Samba 机器，请在 Windows 9x/Me 或 Windows NT/200x 中的控制面板->网络->协议->TCP->WINS 服务器对话框中填入 Samba 机器的 IP 地址。要告诉 Samba 服务器 WINS 服务器的 IP 地址，请在所有 `smb.conf` 文件的 [global] 部分中添加以下行：

```
wins server = <名称或 IP 地址>
```

其中 `<名称或 IP 地址>` 是 WINS 服务器机器的 DNS 名称或其 IP 地址。

不要在作为 WINS 服务器本身的 Samba 服务器的 **smb.conf** 文件中设置这一行。如果你同时设置了 *wins support = yes* 选项和 *wins server = <名称> 选项*，那么 **nmbd** 将启动失败。

有两种设置跨子网浏览的可能场景。第一种详细说明在包含未配置为 Windows NT 域一部分的 Windows 9x/Me、Samba 和 Windows NT/2000 机器的网络中设置跨子网浏览。第二种详细说明在包含 NT 域的网络中设置跨子网浏览。

### 9.5.2 WINS 复制

Samba-3 允许通过 **wrepld** 实用工具进行 WINS 复制。该工具目前未在使用，因为它仍处于开发阶段，并且已经很久没有人维护了。一旦该工具变得适度可用，我们将准备手册页并增强文档的这一部分，以提供使用和技术细节。

### 9.5.3 静态 WINS 条目

向你的 Samba WINS 服务器添加静态条目实际上相当简单。你只需向 *wins.dat* 添加一行，通常位于 */usr/local/samba/var/locks* 或 */var/run/samba*。

*wins.dat* 中的条目采用以下形式：

```
"NAME#TYPE" TTL ADDRESS+ FLAGS
```

其中 NAME 是 NetBIOS 名称，TYPE 是 NetBIOS 类型，TTL 是作为绝对秒数的生存时间，ADDRESS+ 是对应于注册的一个或多个地址，FLAGS 是注册的 NetBIOS 标志。

典型的动态条目如下所示：

```
"MADMAN#03" 1155298378 192.168.1.2 66R
```

要使 NetBIOS 名称变为静态（永久），只需将 *TTL* 设置为 0，如下所示：

```
"MADMAN#03" 0 192.168.1.2 66R
```

NetBIOS 标志可以解释为相加的十六进制值：00 - 广播节点注册，20 - 对等节点注册，40 - 元节点注册，60 - 混合节点注册，02 - 永久名称，04 - 活动名称，80 - 组名称。'R' 表示这是一个注册记录。因此 66R 意味着：混合节点活动且永久 NetBIOS 名称。可以在 Samba 源代码仓库的 **nameserv.h** 头文件中找到这些值。这些是 NB 标志的值。

