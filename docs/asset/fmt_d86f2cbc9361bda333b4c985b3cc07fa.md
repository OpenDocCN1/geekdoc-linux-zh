
```
$ ftp jersey.att.com
Connected to jersey.att.com
220 jersey.att.com FTP server ready.
Name (jersey.att.com; khr): anonymous
331 Guest login ok, send ident as password.
Password: khrorono. maine.edu {not displayed}
230 Guest login ok, access restrictions apply.
ftp> cd /pub/math
250 CWD command successful.
ftp> get primitest
200 PORT command successful.
150 ASCII data connection for primitest (192.11.105.32,2229) (17180 bytes).
226 ASCII Transfer complete.
```

### 终止和取消会话

要终止 `ftp` 会话，在 `ftp` 提示符下输入 `quit`：

```
ftp quit
221 Goodbye.
```

如果远程机器或通信链路故障，你可以使用 `BREAK` 来取消 `ftp` 会话并返回本地机器的 shell。

## 第 9 章：使用 TCP/IP 网络

`226` 传输完成

`local: primetest remote: primetest`

`17180 bytes received in 19 seconds (0.90 Kbytes/s)`

`ftp> quit`

`221 Goodbye`

大文件和软件包通常以压缩 `tar` 格式提供，扩展名为 `.tar.Z`。要使用 `ftp` 传输此类文件，你必须先使用二进制格式。当你从远程系统接收文件时，先使用 `uncompress`，然后使用 `tar` 来恢复原始文件。

第 17 章解释了如何让你的系统通过匿名 FTP 共享文件，以及 `ftp` 的主要用法。许多归档站点存储了成千上万个文件。表 9-1 显示了常用命令及其操作。

### 通过网络浏览器调用 ftp

如果你的系统中安装了 Firefox 或 Mozilla 等浏览器，就不需要使用传统的 `ftp` 命令行界面。当你有网络浏览器时，可以使用如 `ftp://ftp.foobar.com` 格式的 URL 访问匿名 FTP 站点。详情请见第 10 章。

| 符号 | 含义 | 示例 | 效果 |
| --- | --- | --- | --- |
| ! | 指定替换命令的哪个部分 | !cat | 重执行上次 cat 命令 |
| !! | 重执行上一个命令 | !!file | 重执行上一个命令并将输出发送文件 |
| In | 替换历史列表中的第 n 个事件 | | 跳到第三条命令 |
| -n | 替换之前的 n 个事件 | -3 | 回到三个命令之前 |
| !cmd | 替换以 cmd 开头的最后一个命令 | !file:temp | 重执行上一次 find 命令并将输出发送 temp |
| : | 引入参数指定符 | date=1 | 运行 date 并输出到上一次命令的第三个文件 |
| * | 替换所有参数 | cat ls:* | cat 显示上一次 ls 命令列出的文件 |
| $ | 替换最后一个参数 | mv !$ :$ newdir | 将上一个命令的最后一个文件移动到 newdir |
| n | 替换 n 个参数 | rm !$4 1: | 删除上一次命令中命名的第四和第六个文件 |
| s/abc/def/ | 将 abc 切换为 def | !cat:s/kron/korn/ | 重执行上次命令，将 korn 改为 korn |
| ^abc^def | 运行上次命令并将 abc 改为 def | ^oldfile^old_file | 重执行上一个命令，将 oldfile 改为 old_file |

**表 9-1** 最常用的 ftp 命令

### 使用 tftp

另一个可用于在远程主机之间传输文件的命令可用。`tftp` 命令实现了简易文件传输协议 `TFTP`，它使用用户数据报协议 `UDP` 而不是 `ftp` 使用的传输控制协议 `TCP`。当你没有在远程机器上登录时，可以使用 `tftp`。由于 `tftp` 不对用户进行验证，它只能用于传输公共读取的文件。由于 `tftp` 不验证用户身份，它是极不安全的。这意味着它在服务器机器上通常是不可用的。

与 `ftp` 不同，当你使用 `tftp` 时，你并不是与远程主机运行交互式会话。相反，你的系统会在需要时与远程系统进行通信。你通过发布此 `tftp` 命令来启动 `tftp` 会话：

```
$ tftp
tftp> 
```

一旦 `tftp` 会话启动，你就可以发布 `tftp` 命令。通过在 `tftp` 提示符处输入问号 `?` 可以显示 `tftp` 命令列表：

```
tftp> ?Commands may be abbreviated. Commands are:
connect connect to remote tftp
mode set file transfer mode
put send file
get receive file
quit exit tftp
verbose toggle verbose mode
trace toggle packet tracing
status show current status
binary set mode to octet
ascii set mode to netascii
remxt set per-packet retransmission timeout
timeout set total retransmission timeout
? print help information
```

例如，要连接到远程主机复制文件，你使用此 `tftp` 命令：

```
$ tftp
tftp> connect
(to) jersey
```

在你输入 `tftp` 命令 `connect` 后，`tftp` 会给你一个提示符 `"(to)"`。你输入系统名 `jersey`。然后，`tftp` 就会建立到 `jersey` 机器的连接。你也可以在命令行中提供系统名称来建立 `tftp` 会话，如下：

```
$ tftp jersey
```

你可以使用 `tftp status` 命令来确定你 `tftp` 连接的当前状态：

```
tftp> status
connected to jersey
mode: netascii verbose: off tracking: off
remxt-interval: 5 seconds max-timeout: 25 seconds
```

### 使用 telnet 进行远程登录

你可以使用 `login` 登录到远程 UNIX 计算机。然而，你可能想登录到运行其他操作系统的系统，或者不同版本的 UNIX 系统。这可以通过 `telnet` 命令来实现。

要开始 `telnet` 会话，你运行 `telnet` 命令，如下：

```
$ telnet
telnet>
```

一旦建立了 `telnet` 会话，你就可以运行其他 `telnet` 命令。你可以通过输入 `telnet` 命令 `help` 或问号来显示这些命令列表：

```
telnet> help
Commands may be abbreviated. Commands are:
close Close current connection
display display operating system
```

这是响应内容：

Trying...

Connected to michigan

Escape character is '^'

如果你尝试使用 `telnet` 登录到不属于你网络的机器，`telnet` 会搜索数据库。它会告诉你你尝试登录的机器不是网络的一部分。在收到此消息后，你会收到另一个 `telnet` 提示符。

#### 中断和挂起 telnet 连接

你可以通过输入 `telnet` 转义字符后接 `quit` 来中断 `telnet` 连接。这将返回你的本地机器。当你中止到一个通过一系列 `telnet` 命令到达的机器的连接时，你将回到原始机器。

你可以通过输入 `CTRL-Z` 来挂起 `telnet` 连接。当你这样做时，`telnet` 进程将变为后台进程。要激活挂起的 `telnet` 会话，请输入 `fg`。

#### 通过网络浏览器调用 telnet

如果系统中安装了 Netscape Navigator 等网络浏览器，可以通过提供 `telnet:foobar.com` 格式的 URL 来设置 `telnet` 会话。详情请见第 10 章。

### 获取有关用户和主机的信息

在使用远程命令之前，你可能想获取有关网络上机器和用户的信息。你可以使用为此提供的多个命令来获取此类信息，包括 `rwho`、`uptime` 以及 `ping`。你可能还会运行 `traceroute` 来调查网络问题。

#### rwho 命令

你可以使用 `rwho` 命令打印网络上机器上每个用户的信息。你得到的信息包括登录名、主机名、用户所在的位置以及每个用户的登录时间。例如：

```
$ rwho
avi      peg:console    Oct 15 14:53
khr      pokes:console Oct 15 17:32
jmf      arch:tty2     Oct 15 12:21
rrr      homx:tty3     Oct 15 17:06
zeke     xate:tty0     Oct 15 17:53
```

#### finger 命令

你可以使用 `finger` 命令获取任何机器上特定用户的信息。要获取远程主机上用户的信息，请提供该用户的地址。例如，要获取机器 `jersey` 上用户 `khr` 的信息，请使用以下命令行：

```
$ finger khr@jersey
```

在某些机器上，出于安全考虑，禁用了远程用户使用的 `finger` 命令。

#### uptime 命令

你可以使用 `uptime` 命令获取网络上所有机器的状态信息。该命令会打印一个表格，包含本地网络主机的名称、主机是运行还是离机、运行或离机的时间、该主机上的用户数量，以及该机器在过去 5、15 和 15 分钟的平均负载信息。例如：

| 主机 | 状态 | 用户 | 负载 (5m) | 负载 (15m) | 负载 (15m) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| uptime | up 21+02:24, | 6 users | 0.09 | 0.05 | 0.02 |
| bosky | up 20+07:58, | 5 users | 1.23 | 2.08 | 1.87 |
| fickle | up 6+18:48, | 0 users | 1.00 | 0.00 | 0.00 |
| jazzy | up 1+02:31, | 8 users | 4.29 | 0.40 | 3.80 |
| kitsch | up 21+02:06, | 4 users | 1.06 | 1.03 | 1.00 |
| lucky | up 21+02:06, | | 1.09 | 1.04 | 1.00 |
| olympia | up 21+02:05, | 0 users | 1.00 | 1.00 | 1.00 |
| sick | down 2+07:14, | | | | |
| xate | up 2+06:39, | 1 user | 1.09 | 1.20 | 1.57 |

#### ping 命令

在使用 `ping` 命令之前，你可能希望通过该命令来确定远程主机是否可以连接。你可以通过指定主机的地址来 `ping` 远程主机。例如，要 ping 机器 `jersey` 的用户 `khr`，请使用以下命令行：

```
$ ping khr@jersey
```

在某些机器上，`ping khr@jersey` 的输出：

```
from khr@jersey (64 bytes): icmp_seq time=0.05 ms
...
from khr@jersey 64 bytes
```

#### traceroute 命令

`traceroute` 命令用于显示数据包到达远程主机的路径。在大多数现代 Unix 系统中，你可以使用该命令来查看数据包经过的路由器。例如，要查看到达 `jersey` 的路径，可以运行：

```
$ traceroute jersey
```

`traceroute` 命令的输出示例：

```
1  192.168.1.1 (192.168.1.1)  0.523 0.498 0.510 ms
2  10.0.0.1 (10.0.0.1)  1.234 1.210 1.220 ms
3  jersey (172.16.0.1)  2.456 2.432 2.410 ms
```

`traceroute` 输出的每一行代表路径中的一个跳，显示跳数、路由器的名称或 IP 地址以及数据包到达该路由器的往返时间。如果某个路由器没有响应，则会用星号 `*` 表示。

你可以使用选项来调整 `traceroute` 的行为。例如，`-m` 选项可以限制最大跳数：

```
$ traceroute -m 10 jersey
```

`-n` 选项可以跳过 DNS 解析，直接显示 IP 地址：

```
$ traceroute -n jersey
```

## 第二部分：用户网络

如果你使用的系统尚未安装 Secure Shell，你可以从 `http://www.openssh.com/` 获取它。你可以在 `http://www.openssh.com/manual.html` 找到 Secure Shell 命令的帮助页。

### PPP 和 PPPoE

如果你的机器是一个直接连接到互联网的一部分，你可以分别通过 `telnet` 和 `ftp` 远程登录或与这些其他机器交换文件。但如果你的计算机不属于这样的网络呢？在这种情况下，你可以通过特殊协议在普通电话线或 DSL 线路上建立 TCP/IP 连接，普通电话线使用 PPP，DSL 线路使用 PPPoE，它们都支持接入连接。有了这种连接，你需要 PPP 或 PPPoE 客户端软件、一台电话和一个调制解器，或 DSL 线路和一个调制解器，以及来自互联网服务提供商的 PPP 或 PPPoE 账户。许多 UNIX 系统都提供了 PPP 和 PPPoE 软件。
