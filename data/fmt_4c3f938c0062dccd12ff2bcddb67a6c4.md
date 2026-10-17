
## 图 12.6 使用 PrintTool 定义 SMB 打印机

![](img/0a4925a63d7144788f84b23689a2d0da_441_0.png)

图 12.6 中的 `PrintTool` 输入创建了此 `printcap` 条目：

```
lp1:
:sd=/var/spool/lpd/lp1:
:mx#0:
:sh:
:af=/var/spool/lpd/lp1/acct:
:lp1=/dev/null:
:if=/usr/lib/rhs/rhs-printfilters//smbprint
```

使此条目生效的关键是用于该打印机的输入过滤器（`if`）。`smbprint` 是一个使用 `smclient` 打印到远程系统的脚本文件。

在 `PrintTool` 窗口中输入的额外信息用于配置 `smbprint` 脚本。这些信息存储在 SMB 打印机 spool 目录下的 `.config` 文件中。通过查看 `printcap` 文件中的 `sd` 参数可以获取 spool 目录的路径，使用 `cat` 命令可以显示 `.config` 文件的内容：

```
# cat /var/spool/lpd/lp1/.config
share=/var/hawk/hp'
hostip=172.16.15.4
user=craig
password='Wats?Watt?'
workgroup='sybex'
```

## 结语

`.config` 文件包含五个条目，必须按照所示的精确顺序出现。如果未为条目提供值，该条目仍将空条目的形式出现在文件中，例如 `password=''`。这五个条目是：

- `share`：定义共享名称，即远程服务器的 NetBIOS 名称与远程打印机共享名称的组合。
- `hostip`：指定远程服务器的数字 IP 地址。
- `user`：定义用户在远程服务器上的登录名。
- `password`：定义远程服务器访问打印机所需的密码。
- `workgroup`：标识打印机服务器所属的工作组。

如果打印机配置正确且 `.config` 文件包含必要信息，则我们 Linux 系统上的用户应该能够通过输入 `% lpr-lp1 sample.txt` 打印到 `hawk` 上的打印机。我认为这是从 Linux 系统使用 SMB 打印机最简单的方法。

不过，你可以直接通过 `smclient` 软件使用远程打印机。第11章中讨论了使用 `smclient` 访问共享文件，而使用 `smclient` 打印也非常相似。以相同的方式使用 `smclient` 连接到共享，只是这次共享是一个远程打印机。例如：

```
smclient //hawk/hp -U craig%Wats?Watt=-W SYBEX
```

连接到打印机后，使用与传输文件到服务器时相同的 `put` 命令。当 `smclient` 将文件传输到可打印文件时，该文件就会打印。例如，在用 `smclient` 命令连接到 `hp` 打印机后打印 `sample.txt` 文件，输入以下内容：

```
smclient> put sample.txt
```

> 注意：`smclient` 还有一个 `print` 命令，其功能与 `put` 命令相同。通常优先使用 `put`。

![](img/0a4925a63d7144788f84b23689a2d0da_442_0.png)

### 结语

文件和打印机共享是部门网络的基础服务。Linux 是提供这些服务的卓越平台，因为它除了提供 Unix 客户端期望的原生服务外，还能以 Microsoft Windows 客户端期望的格式提供相同的服务。其他部门服务器在将所有客户端集成到单一网络方面没有 Linux 有效。

Linux 擅长的另一个服务是电子邮件。下一章将通过讨论部门邮件服务来结束部门服务器的章节。

# 第3部分

# 第13章 更多邮件服务

部门邮件服务器通常充当邮箱服务器，为客户端保留邮件直到它们准备好下载。Linux 提供了两种邮件的技术：邮局协议（POP），它是传统的邮件协议，以及互联网消息访问协议（IMAP），它正越来越流行。在本章中，我们将使用这两种协议来配置邮件服务器。

除了基本的邮件服务外，Linux 系统还提供了一些你可能需要的用于限制垃圾邮件用户的额外服务。

## 理解 POP 和 IMAP

当 Linux 主机运行 POP 或 IMAP 守护进程时，它可以作为邮件服务器。大多数系统运行两者。除非你采取某些干预措施（例如在安装 Red Hat 6 时选择特定的软件包，然后专门取消选择 POP 和 IMAP），否则 POP 和 IMAP 均可用。

## 添加用户

从左侧滚动菜单中选择 POP 账户（仅限），将在右侧打开用户创建窗口。输入用户名、全名和主目录，点击接受 按钮并为用户输入密码。

用户创建的账户在 `/etc/passwd` 中插入了以下条目：

```
$ grep dan /etc/passwd
dan:BeAvmnE:503:231:Dan Scribner:/home/pop:/bin/false
```

注意该条目与任何其他条目的不同之处在于登录 shell。由于 `dan` 被分配了 `/bin/false`，这意味着 `dan` 无法直接登录服务器。

图13.1 中创建的账户仅限于邮箱访问。尽管 `linuxconf` 称为 POP 账户，但它适用于 POP 和 IMAP。如果你需要创建一个允许用户直接在服务器上读取邮件的账户，请按照第5章的方法使用 `linuxconf`。

### 图 13.1 使用 linuxconf 创建 POP 用户

![](img/0a4925a63d7144788f84b23689a2d0da_445_0.png)

## POP 协议

POP 有两个版本：POP2 和 POP3。POP 协议验证用户的登录名密码并将邮件从服务器移动到用户的本地邮件器。两种协议执行相同的基本功能，但它们并不兼容。POP2 使用端口 109，而 POP3 使用端口 110。Linux 系统自带这两个版本的 POP，但大多数客户端将使用 POP3。

POP3 定义在 RFC 1725。它是一种简单的请求/响应协议：客户端发送命令，服务器对命令做出响应。表13.1 显示了 RFC 1725 定义的 POP3 命令集。

### 表 13.1 POP 命令

| 命令 | 功能 |
| --- | --- |
| `USER username` | 登录所需的用户名 |
| `PASS password` | 登录所需的用户密码 |
| `STAT` | 请求未读邮件数量/字节数 |
| `RETR m` | 获取编号为 `m` 的邮件 |

### 表 13.1 POP3 命令（续）

| 命令 | 功能 |
| --- | --- |
| `DELE m` | 删除编号为 `m` 的消息。 |
| `LAST` | 请求最后访问的消息编号。 |
| `LIST [m]` | 请求消息 `m` 或所有消息的大小。 |
| `RSET` | 取消删除所有消息并将消息编号重置为 1。 |
| `TOP m n` | 打印编号为 `m` 的消息的头部和前 `n` 行。 |
| `NOOP` | 不操作。 |
| `QUIT` | 结束 POP3 会话。 |

根据你对协议和配置的了解，你可以 `telnet` 连接到 POP 端口并测试你的服务器是否有响应。此处显示的 `telnet` 测试证明了守护进程已可用、已安装并准备好运行：

```
% telnet localhost pop-3
Trying 127.0.0.1 ...
Connected to localhost.
Escape character is '^]'.
+OK POP3 almond Server (Version 1.004) ready
quit
+OK POP3 almond Server (Version 1.001) shutdown
Connection closed by foreign host.
```

如果 POP 未准备好运行，`telnet` 测试将返回错误。此示例显示了当 `/etc/services` 文件中没有配置 POP 端口时发生的情况：

```
$ telnet localhost pop-3
pop-3: bad port number
```

检查 `/etc/services` 文件查看实际的 POP 端口。在 Red Hat 6 系统上，你会看到以下 POP2 和 POP3 端口：

```
$ grep 'pop.[2,3]' /etc/services

pop-2 109/tcp postoffice # POP version 2
pop-2 109/udp
pop-3 110/tcp # POP version 3
pop-3 110/udp
```

我从未遇到过端口未定义的问题，但这个 `telnet` 测试显示了另一个问题：
