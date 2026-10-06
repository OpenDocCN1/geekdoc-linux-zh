
第三字段是协议类型，可能包括 `TCP`、`UDP` 或 `RPC/TCP` 或 `RPC/UDP` 中的任何一个。此字段也与 `/etc/services` 中列出的服务的协议类型对应。

第四项是 `wait` 或 `nowait`。通常情况下，`UDP` 是 `wait`，而 `TCP` 是 `nowait`。其中一个例外是 `tftp`，它是 `wait` 的，因为它是一个 `UDP` 数据包，会创建一个伪连接，因此使用 `wait` 以避免竞态条件。`wait` 服务是单线程的，并一直留在等待队列中直到它们终止。`nowait` 服务在建立连接并离开等待队列的同时继续运行，这样另一个服务器就可以绑定到该端口。该条目还可以在小数点后附加一个可选的数字参数，例如 `nowait-400`。这指定了在 60 秒内可以创建的最大服务器数量。如果没有此选项，默认值为 40。

第五字段指定了由 `inetd` 调用时运行服务的用户。这允许以比 `root` 低权限的用户运行服务，具有灵活性。用户字段可以可选以 `user.group` 的形式指定组。如果没有指定组，则使用指定用户的主组。

最后两个字段是程序和程序参数。为程序提供两个字段的灵活性使得能够将实际服务器作为参数调用 `TCP` wrappers 程序。示例中的默认条目使用 `tcp`，来调用实际的守护进程。（参见第 31 章，“`TCP` Wrappers”。）

> 保护服务的两种方法是通过 `TCP` Wrappers 和 `ipchains`（详情见第 30 章，“`IP` 防火墙”）。这两种方法都向受限制的观众提供服务，而不完全停止它们或造成过大的安全风险。

## netstat

对于任何特定主机网络相关问题的最佳故障排除工具是 `netstat`。不带任何选项的 `netstat` 显示网络连接的状态。`netstat` 默认会通过标准解析器和 `/etc/services` 文件解析 `IP` 地址和服务名。

### 读取输出

让我们查看一个不带选项的 `netstat` 输出示例（参见列表 23.4）。

#### 列表 23.4 代表性 netstat 输出（不带服务器）

| 活跃 Internet 连接（不带服务器） | 外地地址 | 状态 |
| 协议 接收-Q 发送-Q 本地地址 | |
| tcp 1 0 127.0.0.1:1061 wolfe.net:www | LAST_ACK |
| udp 0 0 127.0.0.1:domain | * |
| udp 0 0 foo.org:domain | * |
| unix 0 0 localhost:domain | * |
| 活跃 UNIX 套接字（不带服务器） | | |
| 协议 类型 状态 | | |
| unix 1 STREAM CONNECTED 875 0000059 | | |
| unix 1 STREAM CONNECTED 771 0000057 | | |
| unix 1 STREAM CONNECTED 1169 0000069 | | |
| unix 1 STREAM CONNECTED 96 0000002 | | |
| unix 1 STREAM CONNECTED 76 0000001 | | |
| unix 1 STREAM CONNECTED 861 0000054 | | |
| unix 1 STREAM CONNECTED 176 0000006 | | |
| unix 1 STREAM CONNECTED 147 0000085 | | |
| unix 1 STREAM CONNECTED 938 0000062 | | |
| unix 1 STREAM CONNECTED 132 0000064 | | |
| unix 1 STREAM CONNECTED 934 0000061 | | |
| unix 1 STREAM CONNECTED 17 0000003 | | |
| unix 1 STREAM CONNECTED 170 /tmp/X11-unix/X | | |
| unix 1 STREAM CONNECTED 939 /tmp/X11-unix/X | | |
| unix 1 STREAM CONNECTED 835 /tmp/X11-unix/X | | |
| unix 1 STREAM CONNECTED 876 /tmp/X11-unix/X | | |
| unix 1 STREAM CONNECTED 872 /tmp/X11-unix/X | | |
| unix 1 STREAM CONNECTED 864 /tmp/X11-unix/X | | |
| unix 1 STREAM CONNECTED 177 /dev/log | | |
| unix 1 STREAM CONNECTED 148 /dev/log | | |
| unix 1 STREAM CONNECTED 133 /dev/log | | |
| unix 1 STREAM CONNECTED 118 /dev/log | | |
| unix 0 STREAM CONNECTED 107 | | |
| unix 1 STREAM CONNECTED 97 /dev/log | | |
| unix 1 STREAM CONNECTED 77 /dev/log | |

`netstat` 输出的第一行始终提醒你正在查看的是什么：活跃 Internet 连接（不带服务器）。这一行随选项而改变。

第二行包含第一部分的表头。第一列是 `Proto`（协议），通常是 `TCP` 或 `UDP`，也可以是 `raw` 等，取决于你查看的 `/etc/services` 文件中的定义。第三列和第四列分别是 `Recv-Q` 和 `Send-Q`。这分别显示未被连接套接字的程序复制的字节或未被远程主机确认的字节。在 `TCP` 套接字关闭后，经常看到一个字节未被远程主机确认。这是因为连接已关闭，且最后的 `ACK` 未被确认。

接下来的两列分别是本地和外地（远程）地址：它们的格式为 `地址:端口`。在示例中，你看到 `31.ix.net(com.com):1061`（完整域名为了适应空间被截断）连接到 `wolfe.net:www`，你知道那是端口 80。因为 `TCP` 连接了服务器和客户端，它在一个端口发送（80 端口情况），在另一个端口接收（1061 端口）。返回端口没有特别设置。这是一个 1024 以上当前未使用的随机端口。在第一次连接时，客户端告诉服务器它选择了哪个端口，并等待服务器在该端口返回 `SYN` 包，服务器返回 `ACK`，连接即完成——数据开始传输。连接终止时发生的断开也是类似的。这引我们我们最后一列；在这种情况下，它显示 `LAST_ACK`。客户端发送 `LAST_ACK`，当服务器接收到它时，就会丢弃连接。因为不存在连接，所以无法回复。因此，你经常看到

最后一列，即连接状态，可以是以下任何一种：

- `ESTABLISHED`（已建立）
- `SYN_SENT`（已发送 SYN）
- `SYN_RECV`（已接收 SYN）
- `FIN_WAIT1`（等待 FIN1）
- `FIN_WAIT2`（等待 FIN2）
- `TIME_WAIT`（等待等待）
- `CLOSED`（已关闭）
- `CLOSE_WAIT`（等待关闭）
- `LAST_ACK`（等待最后的确认）
- `LISTEN`（监听）
- `CLOSING`（关闭中）
- `UNKNOWN`（未知）

其中一些仅对应于服务器端，另一些仅对应于客户端，但少数几个对应双方。

如果你添加 `-o` 关，你会看到多一列名为 `User` 的列，它会提供创建此连接的进程的用户 `UID` 号。

从下一节开始，你会看到活动 `UNIX` 域套接字（无服务器），然后是标题行。标题行包含 `Proto`（协议）、`RefCnt`（引用计数）、`Flags`（标志）、`Type`（类型）、`State`（状态）、`I-Node`（节点）和 `Path`（路径）。

查看每一列，`Proto` 代表协议，正如你之前看到的：不过，对于 类型 类型套接字，该协议通常是 `UNIX`。

`Ref` 列是已连接进程数的引用计数；它通常为 1，但也可以为 0。

`Flags` 列通常为空白，但如果 `RefCnt` 为 0 且相应的进程正在等待连接请求，该标志可能是 `SO_ACCEPT`，意味着该套接字已准备好接受连接。偶尔，还会出现其他标志，例如代表 `SO_WAITDATA` 的 `W` 或代表 `SO_NOSPACE` 的 `N`。

`Type` 列通常为 `stream`（流式），但也可以是 `DGRAM`、`RAW`、`SEQPACK`、`PACKET` 或 `UNKNOWN`。这些分别对应流式（连接）套接字、数据报（无连接）模式、原始套接字、可靠传输的消息、顺序包、原始接口访问数据包或未知模式（用于未来扩展）。

`State` 列显示套接字的状态；这可以是 `FREE`（空闲）、`LISTENING`（监听）、`CONNECTING`（连接中）、`CONNECTED`（已连接）、`DISCONNECTING`（断开连接）、空白（无记录）或 `UNKNOWN`（未知）。最终状态（`UNKNOWN`）不应该出现。

`I-Node` 列没有特殊意义。它显示与连接对应的 `I-Node`。然而，此 `I-Node` 只有在连接在使用时存在于 `/proc` 中，因此搜索此 `I-Node` 不会得到预期的结果。

最后一列是 `Path`，它显示连接的进程。

之前的示例没有包含常见的连接状态之一：`LISTENING`。这种特定状态只有当 `netstat` 配合 `-a` 开关进行连接时才会显示。使用该开关会更改每个部分标题的第一行。之前你看到的是 Active Internet connections (w/o servers)，现在你看到的是 Active Internet connections (including servers)。第二部分也是如此，现在读为 Active UNIX domain sockets (including servers)。这向我们展示了更长的一个服务器列表，因为包含了那些正在监听连接的服务器（参见列表 23.5）。通过查看，你可以发现某些正在监听请求的进程并没有绑定到端口的守护进程。这是因为 `inet` 守护进程正在监听，并准备根据需要为这些端口生成，例如 `telnet` 端口。

#### 列表 23.5 代表性的 netstat -a 输出（包含服务器）

| Proto | Recv-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- |
| tcp | 1 | *:-wa37-31.i.n:1061 | dgram.wolfe.com:** | LAST_ACK |
| tcp | 0 | *:-wa37-31.i.n.domain | *:* | LISTEN |
| tcp | 0 | *:6000 | *:* | LISTEN |
| tcp | 0 | *:1024 | *:* | LISTEN |
| tcp | 0 | *:mysql | *:* | LISTEN |
| tcp | 0 | *:8411 | ** ** | LISTEN |

```
tcp 0 *:7101 **: LISTEN

tcp 0 *:2849 **: LISTEN

tcp 0 *:7100 **: LISTEN

tcp 0 *:printer **: LISTEN

tcp 0 bar.void:domain **: LISTEN

tcp 0 localhost:domain **: LISTEN

tcp 0 *:finger **: LISTEN

tcp 0 *:auth **: LISTEN

tcp 0 *:rpc **: LISTEN

tcp 0 *:login **: LISTEN

tcp 0 *:shell **: LISTEN

tcp 0 *:telnet **: LISTEN

tcp 0 *:time **: LISTEN

tcp 0 *:daytime **: LISTEN

tcp 0 *:discard **: LISTEN

tcp 0 *:sumprpc **: LISTEN

udp 0 *:stl.wa37-31.ix.domain **:*

udp 0 *:xdmcp **:*

udp 0 *:8388 **:*

udp 0 *:2049 **:*

udp 0 *:1024 **:*

udp 0 bar.void:domain **:*

udp 0 localhost:domain **:*

udp 0 *:ntalk **:*

udp 0 *:talk **:*

udp 0 *:time **:*

udp 0 *:daytime **:*

udp 0 *:discard **:*

udp 0 *:sumprpc **:*

raw 0 *:1 **

raw 0 *:6 **
```

活动 UNIX 域套接字（连接中的服务器）

| Proto | RefCnt | Flags | Type | State | I-Node | Path |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| unix | 0 | [ ACC ] | STREAM | LISTENING | 179 | /var/run/mysql.socket |
| unix | 0 | [ ACC ] | STREAM | LISTENING | 109 | /var/run/gpmctl |
| unix | 0 | [ ACC ] | STREAM | LISTENING | 530 | /dev/log |
| unix | 0 | [ ACC ] | STREAM | LISTENING | 127 | /tmp/.font-unix/fs7100 |
| unix | 1 | [ ] | STREAM | CONNECTED | 875 | 000000569 |
| unix | 1 | [ ACC ] | STREAM | CONNECTED | 143 | fs7101 |
| unix | 1 | [ ] | STREAM | CONNECTED | 871 | 00000057 |
| unix | 1 | [ ] | STREAM | CONNECTED | 169 | 00000059 |
| unix | 1 | [ ACC ] | STREAM | LISTENING | 189 | /tmp/.X11-unix |
| unix | 1 | [ ] | STREAM | CONNECTED | 96 | 00000042 |
| unix | 1 | [ ] | STREAM | CONNECTED | 76 | 00000001 |
| unix | 1 | [ ] | STREAM | CONNECTED | 861 | 00000054 |
| unix | 1 | [ ] | STREAM | CONNECTED | 176 | 00000006 |
| unix | 1 | [ ] | STREAM | CONNECTED | 147 | 00000005 |
| unix | 1 | [ ] | STREAM | CONNECTED | 938 | 00000062 |
| unix | 1 | [ ] | STREAM | CONNECTED | 132 | 00000004 |
| unix | 1 | [ ] | STREAM | CONNECTED | 934 | 00000061 |
| unix | 1 | [ ] | STREAM | CONNECTED | 117 | 00000003 |
| unix | 1 | [ ACC ] | STREAM | CONNECTED | 170 | /tmp/.X11-unix |
| unix | 1 | [ ACC ] | STREAM | CONNECTED | 939 | /tmp/.X11-unix |
| unix | 1 | [ ACC ] | STREAM | CONNECTED | 935 | /tmp/.X11-unix |
| unix | 1 | [ ACC ] | STREAM | CONNECTED | 876 | /tmp/.X11-unix |
| unix | 1 | [ ] | STREAM | CONNECTED | 872 | /tmp/.X11-unix |
| unix | 1 | [ ] | STREAM | CONNECTED | 864 | /tmp/.X11-unix |
| unix | 1 | [ ] | STREAM | CONNECTED | 177 | /dev/log |
| unix | 1 | [ ] | STREAM | CONNECTED | 148 | /dev/log |
| unix | 1 | [ ] | STREAM | CONNECTED | 133 | /dev/log |
| unix | 1 | [ ] | STREAM | CONNECTED | 118 | /dev/log |
| unix | 0 | [ ] | | | 107 | |
| unix | 1 | [ ] | STREAM | CONNECTED | 97 | /dev/log |
| unix | 1 | [ ] | STREAM | CONNECTED | 77 | /dev/log |

如果你添加了 `-v` 开关，可以发现系统中不支持的协议。输出的最后几行是：

```
netstat: not support for AF IPX on this system.

netstat: not support for AF AX25 on this system.

netstat: not support for AF NETROM on this system.
```
