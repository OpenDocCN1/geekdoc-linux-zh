
大多数 ISP 还提供域名服务器、邮件服务器和新闻服务器的 IP 地址。然而，这些地址对于建立 PPP 连接的机制并不重要。

# 使用 pppd 和 chat 创建 PPP 连接

要在两个系统之间建立 PPP 网络连接，你必须在两端都运行 PPP 软件。通常情况下，你的 ISP 会为你提供一个设置好的账户，以便 PPP 软件运行。在拨号连接到远程系统后，会自动启动 PPP 程序。

以下是设置 PPP 连接的两个基本步骤：

- 1. 拨号连接到远程系统。
- 2. 启动 PPP 程序。

正如 `dip` 程序帮助你自动化 SLIP 设置一样，你使用另外两个程序——`pppd` 和 `chat`——来设置和配置 PPP 连接。在尝试任何操作之前，你的 Linux 内核必须包含 PPP 网络设备。

## 第四部分：趣味与利润的 Linux

| 表 18-3（续） |
|---|
| 序列 | 说明 |
|---|---|
| `\n` | 新行符（换行符）字符。 |
| `\N` | 发送空字符（位全零的字节），你不能在 expect 字符串中使用此序列。 |
| `\p` | 暂停十分分之一秒。。你不能在 expect 字符串中使用此序列。 |
| `\q` | 抑制将字符串写入 `/var/adm/syslog` 文件。此序列在 expect 字符串中无效。 |
| `\r` | 回车。 |
| `\s` | 空格字符。当你不想在字符串周围加引号时，请使用此序列。 |
| `\t` | 制表符字符。 |
| `\C` | 与脱字符符号 后的字母对应的控制字符，例如 ^X 意味着 Ctrl-X。 |

你可以在发送字符串（send strings）中使用所有这些转义序列；但正如注释所示，你不能在 expect 字符串（expect strings）中使用许多序列。

## 使用 chat 脚本配合 pppd

PPP 网络的实际细节由 PPP 守护进程 `pppd` 处理，它使用 Linux 内核中的 PPP 驱动代码通过串口端口交换 TCP/IP 数据包。

你需要执行两个基本步骤来完成与远程系统的 PPP 连接：

- 1. 使用你的调制调器拨出，并使用远程系统所有提供的用户名和密码登录远程系统。通常，当你登录远程系统时，该操作应该在远程端启动必要的 `pppd` 软件。
- 2. 在你的系统上启动 PPP 守护进程 (`pppd`)，以与远程系统建立并进行 PPP 会话。

`pppd` 程序设计用于处理这两个步骤。本质上，你使用 `chat` 程序来执行第一步：拨号并登录远程系统。你不需要单独拥有一个 `chat`。相反，你在 `pppd` 命令行中提供一个 `chat` 脚本；`pppd` 会调用 `chat` 来处理该脚本。

# 第 18 章：Linux 中的拨号上网网络

## 一条典型的 pppd 命令行

在最简单的形式下，你可以带一个长命令行运行 `pppd`，其可能如下所示：

```
/usr/lib/ppp/pppd connect /usr/lib/ppp/chat script rtightht modem
defaultroute 192.168.101.111:192.168.102.1 /dev/cua0 38400
```

第一行末尾的反斜杠用于在下一行继续命令。实际的 `pppd` 命令行更长，因为 `chat` 脚本是 expect-send 对序列的一部分。以下是 `pppd` 命令行各个部分的列表：

- `connect` 选项指示 `pppd` 通过执行 `connect` 选项之后双引号内的命令来建立连接。在示例中，命令显示时不包含引号：

`/usr/lib/ppp/chat script`

- `chat` 脚本可能是一长长的 expect-send 字符串对，由 `chat` 程序处理这些字符串。你可以使用以下命令启动 `chat` 来实现一个简单的拨号登录脚本：

```
/usr/lib/ppp/chat ATZ OK AT07555121 CONNECT login: my username \
word: my password
```

- 此 `chat` 脚本发送 `ATZ` 以重置调制调器；等待 `OK` 并发送拨号命令 (`ATphone number`)；等待 `CONNECT` 然后发送一个空字符串（回车符）；等待 `login:` 字符串并发送我的用户名（这应该是你的 PPP 登录名）；最后，等待 `word:` 字符串并发送我的密码（你的 PPP 登录账户的密码）。
- `cts` 选项指示 `pppd` 使用请求发送（RTS）和清除发送（CTS）信号与调制调器进行硬件交互。有关 RTS 和 CTS 信号的更多信息，请参考第 15 章“调制调器”。
- `defaultroute` 选项指示 `pppd` 在你的系统上设置默认路由，将远程系统作为网关。如果你已经设置了默认路由（例如你的以太网局域网），`pppd` 不将默认路由设置为远程系统。
- 两个 IP 地址指示 `pppd` 使用 IP 地址 `192.168.101.111` 作为本地接口，使用 IP 地址 `192.168.102.1` 作为 PPP 连接的远程端。如果远程主机动态分配 IP 地址，你可以使用 `0.0.0.0` 作为你的本地 IP 地址；`pppd` 会自动使用远程系统分配的 IP 地址。
- 设备名称告诉 `pppd` 在设备 `/dev/cua0` (COM1) 上拨出。如果你的调制调器在 COM2 上，请使用 `/dev/cual` 作为设备名称。
- 最后一个选项导致 `pppd` 将调制调器的数据速率（通常称为波特率）设置为 38,400 bps。

你应该注意关于 `pppd` 命令行的一个关键点：整个 `char` 命令（紧随 `connect` 选项）被包含在引号中，但 `chat` 命令本身使用了各种带引号的字符串。你必须记住为这些嵌入的引号加上反斜字符前缀。以下示例显示了 `chat` 脚本在 `pppd` 命令行中的样子：

```
/usr/lib/pppd/pppd connect "/usr/lib/pppd/chat \" ATZ OK ATDT551251
CONNECT: my-username password: my-password (rest of command line not shown)
```

## 第四部分：使用 Linux 娱乐与盈利

你应该能在末尾找到列出的 `ppp0` 设备。`ifconfig` 的输出还显示了 PPP 连接本地端和远端的 IP 地址。此输出确认了 PPP 设备已启动并运行。

要验证路由表设置是否正确，请在不带任何参数的情况下使用 `/sbin/route` 命令，如下所示：

在路由表中，第一行显示了通往 PPP 连接远端的路由；它应该指向 `ppp0` 设备。此外，还应该设置默认路由，使 PPP 连接的远端作为你系统的网关（如路由表的最后一行所示）。

在检查了接口配置（使用 `ifconfig` 命令）和路由表（使用 `route` 命令）后，你应该验证自己是否可以访问到一些知名主机。如果你的 ISP 提供了名称服务器或邮件服务器的 IP 地址，你可以 `ping` 那些地址。否则，尝试 `ping` 你工作场所或大学某个系统的 IP 地址。

下面的示例展示了当你尝试运行 `ping` 命令时会看到的内容：

```
ping 140.90.23.100
PING 140.90.23.100 (140.90.23.100): 56 data bytes
64 bytes from 140.90.23.100: icmp_seq=0 ttl=224 time=336.0 ms
64 bytes from 140.90.23.100: icmp_seq=1 ttl=224 time=290.2 ms
64 bytes from 140.90.23.100: icmp_seq=2 ttl=224 time=350.2 ms
64 bytes from 140.90.23.100: icmp_seq=3 ttl=224 time=300.2 ms
64 bytes from 140.90.23.100: icmp_seq=4 ttl=224 time=340.2 ms
64 bytes from 140.90.23.100: icmp_seq=5 ttl=224 time=290.2 ms

--- 140.90.23.100 ping statistics ---

6 packets transmitted, 6 packets received, 0% packet loss
round-trip min/avg/max = 290.2/317.8/350.2 ms
```

每行的末尾显示了数据从你的系统到达指定 IP 地址（在本例中为 140.90.23.100）返回你的系统的往返时间。对于通过拨号的 PPP 连接，你会看到数百毫秒级的时间。

顺便提一下，你不需要在某个系统上有账号才能 `ping` 它的 IP 地址。虽然系统可能会禁用自动响应 `ping` 消息（`ping` 使用互联网控制消息协议或 ICMP 消息），但大多数系统都会响应 `ping`。

## 第 18 章：Linux 中的拨号网络

### 结束 PPP 连接

在 `pppd` 建立 PPP 连接后，只要两端的 PPP 软件继续运行，链路就会保持。当你不再需要 PPP 连接时，可以通过停止 `pppd` 进程来结束它。
