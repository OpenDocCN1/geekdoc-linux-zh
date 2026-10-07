
`os level=` 的默认值随着 Samba 版本而变化。`2.0.6` 将此参数默认设置为 `20`，而 `2.0.5` 默认设置为 `0`。在 Samba `2.1` 中，默认设置为 `32`，与 NT 持平。`os level=` 的最大值为 `255`。

## local master=

该参数默认值为 `yes`。如果此参数设置为 `yes`，则允许 Samba 服务器赢得浏览器选举，但不保证一定能赢得。如果此参数设置为 `no`，Samba 服务器无法赢得浏览器选举。从以下 `smb.conf` 开始：

```
encrypt passwords=yes
workgroup=mygroup
preferred master=yes
os level=255
[tmp]
path=/tmp
```

在一个虚拟终端上运行 `tail -fn0 log.memb`，并在另一个终端上重启 Samba。注意 30 秒后，Samba 服务器赢得了浏览器选举。在 `smb.conf` 顶部添加以下行并重启 Samba：

```
local master=no
```

注意，这次 Samba 服务器没有赢得浏览器选举。

## wins support=

从以下 `smb.conf` 开始：

```
encrypt passwords=yes
workgroup=mygroup
[tmp]
path=/tmp
```

在一个虚拟终端上运行 `tail -fn0 log.memb`，并在另一个终端上重启 Samba。注意 30 秒后，Samba 服务器赢得了浏览器选举。在 `smb.conf` 顶部添加以下行并重启 Samba：

```
local master=no
```

注意，这次 Samba 服务器没有赢得浏览器选举。

> 注意
>
> 上述消息仅在 Samba 服务器赢得浏览器选举时才会出现。你可以通过包含 `os level=255` 来确保获胜（请参见下一节）。

## domain=

> 上述消息仅在 Samba 服务器赢得浏览器选举时才会出现。你可以通过包含 `os level=255` 来确保获胜（请参见下一节）。

## string=

> 上述消息仅在 Samba 服务器赢得浏览器选举时才会出现。你可以通过包含 `os level=255` 来确保获胜（请参见下一节）。

## interfaces=

> 上述消息仅在 Samba 服务器赢得浏览器选举时才会出现。你可以通过包含 `os level=255` 来确保获胜（请参见下一节）。

## load printers=

默认值为 `yes`。但如果此参数设置为 `no`，打印队列将不会出现在浏览器中。

# announce as= 和 announce version=

这些参数决定了 Samba 服务的 `nmbd` 守护进程如何宣告自己。

除非在极特殊的情况下，否则它们应该保持默认值。

# lm announce= 和 lm interval=

默认值分别为 `auto` 和 `60`，这适用于大多数情况。`auto` 设置意味着除非接收到广播（通常来自 OS/2 客户端），否则不会进行 LAN 管理器（LANMAN）宣告广播。`lm announce=no` 设置意味着“无论如何都不进行广播”，而 `lm announce=yes` 意味着“一定广播”。`lm announce=auto` 在处理 OS/2 客户端或其他发起 LANMAN 广播的主机时表现与 `lm announce=no` 类似。

`lm_interval=` 参数决定了服务器发送这些广播的频率。

# 共享级浏览参数 (Share-Level Browsing Parameters)

`browseable=` 和 `comment=` 参数影响特定的共享。

`browseable=` 参数值为 `yes`。如果设置为 `no`，则防止显式指定的共享在浏览列表中显示。你可以通过切换 `[tmp]` 的 `browseable=` 参数进行实验。注意，它在总线上的显示是可以切换的。但是，无论 `browseable=` 设置为什么，都可以通过 `net` 命令进行访问。

`comment=` 参数等于全局服务器 `string=` 参数。其字符串值会显示在浏览器上，包括 `net view \servername`。

# 浏览理论 (Browsing Theory)

该理论认为本地主浏览器（local master browser）发送浏览列表。当任何客户端发送浏览请求时，本地主浏览器会将浏览列表发送给该客户端。要看到它们的运行过程，请运行 `tcpdump` 并访问服务器。最好使用 Samba 项目提供的特殊 `tcpdump` 程序，因为它能以易读的形式显示 SMB 数据包。第一步是找到快长度（snap length）。快长度是 `tcpdump` 中的 `-s` 选项，它决定了数据包的最大。为了实验目的，你希望快长度恰好足够容纳整个返回浏览列表。运行以下命令：

```
$ tcpdump -s500 port 138 or port 139 | grep -i snap
```

然后，从 Windows 机器运行以下命令：

```
$ net view \servername
```

如果你从通过 `grep` 过滤的 `tcpdump` 命令中退出，意味着你收到了“增加快长度”的消息，因此请增加快长度。如果没有输出，则减小快长度。继续此直到快长度比消除快长度消息所需的最小长度大几字节。现在你准备好将输出重定向到文件了。执行以下操作：

```
$ tcpdump -s500 port 137 or port 138 or port 139 > tst.t
```

上述命令在所有 Samba 端口上列表，并将结果转储到名为 `tst.t` 的文件中。一旦开始运行，从 Windows 服务器执行以下命令：

```
$ net view \servername
```

等待 10 秒让 Windows 命令完成，然后在 `tcpdump` 命令上按 Ctrl+C 退出。在 `less` 分器中查看 `tst.t`。你将看到多个数据包从客户端发送到服务器，反之亦然，然后设置协议。

接下来，你将看到一个从客户端到服务器的 IP 数据包，其中包含一个类型为 `SMBtrans (REQUEST)` 的 SMB 数据包。紧接着是一个从服务器发送到客户端的 IP 数据包，其中包含一个类型为 `SMBtrans (REPLY)` 的 SMB 数据包。这是一个巨大的数据包，如果你查看 `dump` 数据包的十六进制部分，将看到浏览列表。这就是 Samba 服务器向客户端提供 Windows 列表的方式。

同样，你还会看到来自 Windows 客户端的选举请求以及随后的事务。从一个没有本地主服务器运行的 Samba 服务器开始（设置 `preferred master=no` 并重启 Samba）。将 `tcpdump` 端口转储到文件中；部分在 Windows 客户端上运行 `net view /workgroup:workgroup`。让它运行 40 秒，然后按 Ctrl+C 退出 `tcpdump`。

客户端向服务器发送大量的 `[MAILSLOT]BROWSE` 请求。在处理了一系列请求后，服务器最终返回了（例如在设置后 17 秒后）一个在 SMB 数据包名称中带有 `__BROWSE__` 的注册包。注意，这里的“返回”并不完全准确，因为服务器是广播该数据包。

结论是，数据包嗅探是故障排除和深入 NetBIOS 通信过程极极方法。

# 浏览故障排除 (Browsing Troubleshooting)

浏览的故障排除可能很困难。为了简化操作，本节确定了一种故障排除策略，旨在通过先执行快速测试来尽量短到达解决方案的时间：

## 本地子网浏览 (Local-Subnet Browsing)

- 确定 `testparm` 是否产生任何错误。
- 确定服务器控制台上的共享是否可浏览。
- 确定该共享是否设计为可浏览。
- 确定 Windows 命令行上的共享是否可浏览。
- 解决命名问题。

本节随后将讨论浏览的其他其他用故障排除技巧。

### 确定 testparm 是否产生任何错误

`testparm` 程序运行非常快，可以立即使用。查找 `testparm` 显示的任何错误或警告：

```
[rootminserver /root]# testparm
Loading smb config /etc/samba/smb.conf
Loaded added config from /etc/samba/smb.conf

No errors found.
```

### 确定共享在服务器控制台上是否可浏览

下一步也很快。在服务器控制台上观察可浏览性：

```
$ localhost
```

### 确定该共享是否设计为可浏览

如果前面的命令没有显示该共享，请跳过本节。

### 确定共享在 Windows 命令行上可浏览

从 Windows 客户端尝试以下命令：

```
C:\WINDOWS>net view \\mainserv
```

### 解决命名问题

如果对连接性仍有疑问，请在客户端和服务器之间运行 ping，并解决阻碍 ping 的任何问题。

```
MAC Address = 00-00-00-00-00-00

:\WINDOWS>
```

`_MSBROWSE_` 的存在表示存在本地主浏览器（local master browser），工作组名称的 `<ID>` 版本也表示本地主浏览的存在。如果不存在本地主浏览器，这两个条目将不会出现。

如果前面的命令报错，请尝试使用大写的 -A 选项配合 IP 地址重试：

```
C:\WINDOWS>nbtstat -n A 192.168.100.101
```

# NetBIOS 远程机器名称表

| 名称 | 类型 | 状态 |
|---|---|---|
| MAINSERV | <00> | UNIQUE Registered |
| MAINSERV | <03> | UNIQUE Registered |
| MAINSERV | <20> | UNIQUE Registered |
| ...MSBROWSE | <01> | GROUP Registered |
| TEST11 | <00> | GROUP Registered |
| TEST11 | <1D> | UNIQUE Registered |
| TEST11 | <1E> | GROUP Registered |

```
MAC Address = 00-00-00-00-00-00

:\WINDOWS>
```

注意，无法通过 NetBIOS 名称访问服务器本身就是一个必须纠正的问题。

有时，通过 Windows 命令行提示符执行以下命令可以触发浏览选举（browse election）：

```
C:\WINDOWS>net view /workgroup:test11
```

```
错误 6118：无法找到此工作组中共享资源的计算机。计算机可能已重启。请等几分钟重试。如果问题仍然存在，请确保你的网络适配器设置正确。

C:\WINDOWS>
```

在前面的命令中，响应表示错误。该错误是由缺少本地主浏览器引起的。然而，前面的命令有时会有触发浏览选举的副作用。通常在执行前面的命令后 30 秒内，`nbtstat -n -a servername` 命令将指示本地主浏览器的存在。

以下是一个确定本地主浏览器的 UNIX 命令：

```
nmblookup -SM
```

如果 Samba 服务器上存在本地主浏览器，该命令的输出与 `nbtstat -n -a servername` 相同；否则，它会注释无法找到 `_MSMBROWSE_`。

在 Samba 服务器上，可以通过以下命令实时显示本地主浏览器的注册（以及它当选的域主）：

```
$ tail -fn0 nmb.log
```

该命令将输出到 log.nmb 文件，其中包含本地主浏览器的注册信息。

# 针对浏览问题的其他排排除策略

排除浏览问题的策略有很多。本节将讨论几种最可能揭示问题根源的策略。

# 创建可靠的本地主浏览器

一个实用的策略是修改 `smb.conf` 以强制在重启 30 秒后进行浏览器选举。在全局部分中包含这三个参数：

```
local master=yes
preferred master=yes
os level=255
```

> 注意
>
> 前面的命令会破坏任何现有的 NT 或 Samba 本地主浏览器。仅当此类不会造成损害或不便时才使用前面的命令。

重启 Samba，然后通过 `tail -fn0 servername` 确认 Samba 服务器是否在 30 秒内变成了本地主浏览器。

# 切换 wins 支持：

取决于其他因素，`wins support=` 可能会对浏览问题产生影响。在不会损害网络稳定性或给用户带来不便的情况下，切换 `wins support=` 并重启 Samba。

# 寻找可浏览共享并利用差异

如果一个共享出现在浏览列表中，而另一个没有，请利用这些差异。更改共享以使它们彼此相似，直到你找到浏览问题的根源。

在执行此项操作时，让本地主浏览器处于一致状态非常重要；因此，务必添加前面提到的三行，以便在 30 秒内启动一个可靠的本地主浏览器。

# 始终寻找其他测试来缩小问题范围

故障排除的核心在于缩小，而不是发现。发现是结果。通常寻求测试来缩小问题范围，解决方案最终会显现出来。

## 总结

浏览（Browsing）是指客户端在列表中显示 SMB 共享的行为。共享的可浏览性由其 `browseable=` 参数决定。这与访问性（accessibility）形成对比，后者是通过显式命名共享来读取或写入共享中文件的能力。共享可以是可浏览且可访问、可浏览但不可访问、不可浏览但可访问，或不可浏览且不可访问。通常，预期为可浏览的共享由于网络、本地主浏览器或 SMB 客户端的问题而没有出现在浏览列表中。

对浏览环境影响最大的全局参数是 `workgroup=`、`netbios name=`、`preferred master=`、`os level=`、`local master=`、`wins support=` 和 `auto services`。某些参数在章节中也讨论过。

当客户端向本地主浏览器请求列表并接收该列表时，就会浏览。可以通过 topdump 数据包观察程序看到。

当发生问题时，减少找到解决方案时间的方法是从简单的测试开始，然后逐渐转向困难的测试。你使用的方法如下：

- 运行 `testpar`。
- 共享在服务器控制台上是可浏览的吗？
- 该共享被设计为可浏览的吗？

# 跨子网浏览

### 第 33 章

与 NetBEUI 不同，IP 是一种完全可路由协议，这就是为什么大多数关于 SMB 服务的文档都建议您在网络中仅使用 TCP/IP。本章假设在提供或使用 SMB 服务的系统中，仅使用了 IP。

## 注意

在存在 Samba 服务器或客户端的网络中，在 Windows 系统上启用 NetBEUI 或 IPX 不会引入多个、异异的主浏览器（一个 NetBEUI，一个 IP），并可能导致许多系统在跨子网（甚至在同一子网内）上无法访问。

最后，请理解本章仅处理子网与子网之间的 SMB 通信。跨子网浏览的额外要求还包括：适当的 IP 子网设置、IP 路由、IP 名称服务（例如域名系统系统，即 DNS）以及其他非 Samba 的 IP 网络服务。此类概念和细节超出了本书的范围（可能可以写好几本书），但对于涵盖这些主题的正确 TCP/IP 通信来说，它们是必不可少的，并将帮助您进一步诊断不涉及 Samba 但会影响其正常运行的问题。

## 注意

即使是配置恰当的 Samba 服务器，如果网络之间的底层 IP 服务（如 DNS、路由等）没有正确设置，也将无法进行通信。

作为快速参考，表 33.1 列出了 InterNIC 在其征求意见（RFC）文件中定义的标准 IP 子网类和可用私有网络。永远不要未标记为“私有”的子网，除非该子网已向 InterNIC 注册供组织使用。

## 高级 Samba

第四部分

| 表 33.1 类 | 子网（数量） | 子网掩码 | 最大节点数 | 私有子网 |
|---|---|---|---|---|
| A | 1.x.x.x.-127.x.x.x | 255.0.0.0 | 1670 万 | 10.x.x.x (1) |
| B | 128.x.x.x.-191.x.x.x | 255.0.0.0 | 65,534 | 172.16.x.x.-172.31.x.x (16) |
| C | 192.x.x.x.-223.x.x.x | 255.255.255.0 | 254 | 192.168.0.x.-192.168.255.0 (256) |
| D, F | 224.x.x.x.-255.x.x.x | 异 | 异 | 无 |

# 浏览器与控制器的区别

原生 Windows 服务器仅理解工作组（workgroups）和域（domains），每个域包含一组预定义的浏览列表和认证控制服务。对于这些 Windows 服务器来说，这些者是不可分割的。Samba 服务器将浏览列表与认证控制分离，这为每个部分提供了更多的选项和更强的控制力。因此，即使是最经验丰富的 Windows 服务器管理员也应该重新熟悉浏览列表和认证控制，事实上，它们是相互分离的。

> 提示：通过将浏览器功能与控制器功能分离，仅浏览器的 Samba 服务器相比原生 Windows 服务器有一个优势，即去除了控制器带来的额外认证负载。这增加了可靠性和性能，因为域的主浏览器除了管理服务器列表之外，不需要管理服务器和用户账户（更不用说它们的各种认证服务，如域登录等）。

## 浏览器服务

任何子网内或子网之间通信的关键在于维护一个系统及其能力的列表。CIFS/SMB 服务维护任何工作组或域中所有系统的浏览列表。

工作组中的原生 Windows 器和客户端无法访问其所在子网之外的其他系统。对于多个子网，Windows 引入了域（domain）的概念（通常称为 [Windows] NT 域，以免与 DNS 或 NIS 域混淆）。域控制器——无论是主域控制器（PDC）还是备用域控制器（BDC）——都负责同步域内所有子网之间的浏览列表。因此，对于原生 Windows 服务器，维护多个子网至少需要一个 PDC。

### Windows NT 的损失，Samba 的收获
